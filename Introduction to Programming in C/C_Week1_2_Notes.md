# 📘 NPTEL — Introduction to Programming in C
### Prof. Satyadev Nandakumar | IIT Kanpur
### Exam-Ready Notes: Week 1 & Week 2

---

## Table of Contents
1. [Algorithms, Flowcharts & the Programming Process](#1-algorithms-flowcharts--the-programming-process)
2. [C Program Structure & Compilation Cycle](#2-c-program-structure--compilation-cycle)
3. [Variables, Assignment & Sequential Execution](#3-variables-assignment--sequential-execution)
4. [The `for` Loop](#4-the-for-loop)
5. [Nested Loops (Double Loops)](#5-nested-loops-double-loops)
6. [The `break` Statement & Infinite Loops](#6-the-break-statement--infinite-loops)
7. [The `continue` Statement](#7-the-continue-statement)
8. [Flag Variables (Alternative to `break`/`continue`)](#8-flag-variables-alternative-to-breakcontinue)
9. [`scanf` Return Value & Input Termination](#9-scanf-return-value--input-termination)
10. [GCD — Euclid's Algorithm (Case Study)](#10-gcd--euclids-algorithm-case-study)
11. [Matrix Trace (Nested `for` Loop Case Study)](#11-matrix-trace-nested-for-loop-case-study)
12. [Pythagorean Triples (Multi-variable `continue` Case Study)](#12-pythagorean-triples-multi-variable-continue-case-study)
13. [`getchar` vs `scanf %c` for Characters](#13-getchar-vs-scanf-c-for-characters)
14. [The Comma Operator in `for` Loops](#14-the-comma-operator-in-for-loops)
15. [`if` and `if-else` Statements](#15-if-and-if-else-statements)
16. [Operators — Modulo, Logical AND/OR/NOT, Leap Year](#16-operators--modulo-logical-andornot-leap-year)
17. [Variables & Data Types — `int`, `float`, Format Specifiers](#17-variables--data-types--int-float-format-specifiers)
18. [Tracing Programs — `printf`, `\n`, Comments](#18-tracing-programs--printf-n-comments)
19. [`while` Loop — Structure, Sentinel Pattern, Priming Read](#19-while-loop--structure-sentinel-pattern-priming-read)
20. [Loop Invariants](#20-loop-invariants)
21. [`do-while` Loop](#21-do-while-loop)
22. [Longest Contiguous Increasing Subsequence (LCIS)](#22-longest-contiguous-increasing-subsequence-lcis)
23. [GCD with `while` Loop — Full Implementation & Loop Invariant](#23-gcd-with-while-loop--full-implementation--loop-invariant)
24. [Matrix Row-Sum-Squared Problem](#24-matrix-row-sum-squared-problem-nested-while-loops)
25. [🧪 Assignment 1 Analysis](#-assignment-1-analysis)
26. [🧪 Assignment 2 Analysis](#-assignment-2-analysis)

---

## 1. Algorithms, Flowcharts & the Programming Process

📅 **Week 1**

### Concept Summary
An **algorithm** is a finite, step-by-step procedure to solve a problem. Before writing C code, you define the problem, design an algorithm (optionally as a flowchart), and then implement it. A flowchart uses standardized shapes: **oval** = start/end, **parallelogram** = input/output, **rectangle** = operation, **diamond** = decision/test.

### Key Syntax / Rules Box
```
[Algorithm → Flowchart → C Code]
```
- Algorithms must be **finite** (they must terminate).
- Every decision diamond has exactly **two exits**: true/false (yes/no).
- Variables are "named boxes" — they hold exactly **one value at a time**.
- Algorithms are analogous to cooking recipes, but must be **unambiguous**.

### Detailed Code Example
```c
// Flowchart translated to C: Sum of first N numbers
#include <stdio.h>
int main() {
    int n, i, sum;
    scanf("%d", &n);     // INPUT: read N
    sum = 0;             // Initialize accumulator
    i = 1;               // Counter starts at 1
    while (i <= n) {     // LOOP CONDITION (diamond in flowchart)
        sum = sum + i;   // OPERATION (rectangle)
        i = i + 1;       // Update counter
    }
    printf("%d\n", sum); // OUTPUT (parallelogram)
    return 0;
}
```
**What would NPTEL ask about this?**

❓ What is the value of `sum` if `n = 0`?
✅ `sum = 0`
💡 The while condition `i <= n` is false immediately (1 <= 0 is false), so the body never executes; `sum` stays 0.

❓ What happens if `sum` is not initialized before the loop?
✅ Undefined behaviour — `sum` contains **garbage value**.
💡 Uninitialized variables in C don't default to 0; this is a classic NPTEL trap.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Not initializing `sum = 0` | Garbage output | Always initialize accumulators |
| Loop condition `i < n` instead of `i <= n` | Sums only 1 to n-1 | Use `i <= n` to include n |
| Off-by-one: starting `i = 0` | Adds 0 into sum (harmless here, but wrong in products) | Start `i = 1` for sum of first N naturals |

### Quick Recall
- Algorithm = finite steps → flowchart = visual → C = implementation
- Diamond = decision, Rectangle = action, Parallelogram = I/O
- Variables store exactly **one value at a time**

---

## 2. C Program Structure & Compilation Cycle

📅 **Week 1**

### Concept Summary
Every C program must have a `main()` function — execution always starts there. The edit-compile-run cycle is fundamental: write → `gcc` → `./a.out`. The preprocessor directive `#include <stdio.h>` must be present for any input/output (`printf`, `scanf`). Statements end with a **semicolon**; blocks are wrapped in **curly braces `{}`**.

### Key Syntax / Rules Box
```c
#include <stdio.h>       // MUST include for printf/scanf

int main() {             // ALL programs start here; no space before {
    printf("Welcome to C\n");  // Statement ends with semicolon
    return 0;            // Signals successful termination
}
```
- Compile: `gcc filename.c` → produces `a.out`
- Run: `./a.out`  ← the `./` is mandatory on Linux
- Compilation errors → **no executable is produced**
- Logical errors (wrong output) → no compiler warning, must be debugged manually

### Detailed Code Example
```c
#include <stdio.h>       // Preprocessor: includes standard I/O library

int main() {             // Program entry point
    printf("Hello!\n");  // \n = newline character
    return 0;            // Return 0 = success to OS
}
```
**What would NPTEL ask about this?**

❓ What does the compiler produce if there are no errors?
✅ An executable file named `a.out`
💡 The compiler produces **no output on the terminal** when compilation succeeds — silence = success.

❓ What is the purpose of `#include <stdio.h>`?
✅ Includes the Standard Input/Output library needed for `printf` and `scanf`.
💡 Omitting it → compiler error (or warning) because `printf` is unknown.

❓ What happens if the semicolon after `printf(...)` is missing?
✅ Compilation error — C statements **must** end with `;`.
💡 The compiler reports a syntax error, often on the **next line** (confusing beginners).

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Missing `#include <stdio.h>` | Compiler error: `printf` undeclared | Always include it |
| Running as `a.out` (no `./`) | Shell: "command not found" | Use `./a.out` |
| Missing `}` for main | Compilation error | Match every `{` with `}` |
| Using `notepad` (Windows) | Saves as `.txt`, not `.c` | Use Notepad++, VSCode, etc. |
| Unclosed `"` in `printf` | Syntax error | Close all double quotes |

### Quick Recall
- `#include <stdio.h>` → always first line
- `int main()` → program starts here
- `gcc file.c` → compile; `./a.out` → run
- Every statement ends with `;`

---

## 3. Variables, Assignment & Sequential Execution

📅 **Week 1**

### Concept Summary
A variable is a **named memory box** holding exactly one value at a time. The **assignment operator `=`** takes the right-hand side value and stores it in the left-hand variable, overwriting whatever was there. Multiple assignments executed in sequence are processed **top to bottom, one at a time**.

### Key Syntax / Rules Box
```c
int a, b, g;        // Declare three integer variables
a = 10;             // a = 10
b = 6;              // b = 6
g = a % b;          // g = 10 mod 6 = 4  (% is modulo in C)
a = b;              // a = 6  (old value of a is LOST)
b = g;              // b = 4
```
- `=` is **assignment**, NOT equality. Equality test is `==`.
- Right-hand side is **evaluated first**, then stored in left-hand side.
- **Swap pattern** requires a temporary variable: `t = a; a = b; b = t;`
- `%` is the **modulo operator** (remainder after integer division).

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int a = 10, b = 6, g, t;

    // SWAP a and b (if a < b, ensure a is larger)
    if (a < b) {
        t = a;   // Step 1: Save a in temp
        a = b;   // Step 2: Overwrite a with b
        b = t;   // Step 3: Overwrite b with saved a
    }
    // Now a >= b guaranteed

    g = a % b;   // g = remainder(10, 6) = 4
    printf("g = %d\n", g);   // Output: g = 4
    return 0;
}
```
**What would NPTEL ask about this?**

❓ After `a = b; b = a;` (NO temp), what are a and b if initially a=5, b=3?
✅ Both become 3.
💡 `a = b` makes a=3; then `b = a` makes b=3. The original value 5 is **lost**. Always use a temp for swaps.

❓ What does `g = a % b` give when a=18, b=6?
✅ `g = 0`
💡 18 ÷ 6 = 3 exactly, remainder 0. This signals the GCD algorithm to stop.

❓ What is `7 % 3`?
✅ `1` (since 7 = 3×2 + 1)
💡 `%` gives the **remainder**, not the quotient.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `a = b; b = a;` (swap without temp) | Both variables hold b's value | Use `t = a; a = b; b = t;` |
| `if (a = b)` instead of `if (a == b)` | Assignment inside if; always true/false based on b | Use `==` for comparison |
| `int a;` then using `a` without init | Garbage value (UB) | Always initialize |

### Quick Recall
- `=` assigns; `==` tests equality
- Swap needs 3 steps + temp variable
- `%` = remainder; `a % b = 0` means b divides a exactly
- Sequential: statements execute **top to bottom**

---

## 4. The `for` Loop

📅 **Week 2**

### Concept Summary
The `for` loop bundles initialization, test, and update into one line — making it the **preferred loop when the number of iterations is known in advance**. It is equivalent to a `while` loop but more readable and compact. The initialization runs **once**; the test runs **before each iteration**; the update runs **after each iteration body**.

### Key Syntax / Rules Box
```c
for (init_expr; test_expr; update_expr) {
    // body
}

// Equivalent while loop:
init_expr;
while (test_expr) {
    // body
    update_expr;
}
```
- `init_expr` executes **exactly once** at the start.
- `test_expr` is checked **before** every iteration (including the first).
- `update_expr` executes **after** the body, **before** re-testing.
- If `test_expr` is **false from the start**, the body never executes.
- Multiple variables can be initialized using the **comma operator**: `for (sum=0, i=1; ...)`

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    float reciprocal_sum = 0.0;  // Must be float; 1/i is a fraction
    int i;

    // Sum of 1/1 + 1/2 + ... + 1/100
    for (i = 1; i <= 100; i = i + 1) {  // init; test; update
        reciprocal_sum = reciprocal_sum + 1.0 / i;
        // Use 1.0/i NOT 1/i: integer division 1/i = 0 for i > 1!
    }
    printf("Sum = %f\n", reciprocal_sum);
    return 0;
}
```
**What would NPTEL ask about this?**

❓ What does `for (i = 0; i < 5; i++)` print if body is `printf("%d ", i);`?
✅ `0 1 2 3 4`
💡 Loop runs while `i < 5`; i goes 0,1,2,3,4. When i=5, test fails — 5 is **not** printed.

❓ What is the value of `i` after `for (i = 0; i < 10; i++) { if (i % 2 == 1) break; }` ?
✅ `i = 1`
💡 i=0: 0%2=0, no break, update i=1. i=1: 1%2=1, break immediately. **Update does NOT run on break** — i stays 1, not 2.

❓ If `reciprocal_sum` uses `1/i` instead of `1.0/i`, what happens for i=2?
✅ `1/2 = 0` (integer division), so 0 is added — **wrong answer**.
💡 In C, dividing two integers always gives an integer. Use `1.0/i` or `(float)1/i`.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `1/i` with int `i` | Integer division → 0 for i > 1 | `1.0/i` or cast `(float)1/i` |
| `i <= 100` vs `i < 100` | Off-by-one: includes or excludes 100 | Know your boundary |
| Modifying `i` inside the body | Unexpected loop behaviour | Avoid changing loop variable inside body |
| `for (i=0; i<n; i++)` with `n` uninitialized | Garbage iteration count | Initialize `n` before the loop |

### Quick Recall
- `for (init; test; update)` — 3 parts in one line
- Init: once. Test: before each. Update: after each body.
- `break` → exits loop **without** running update
- `continue` → skips body, **runs update**, then tests
- Use `for` when iteration count is known; `while` when it isn't

---

## 5. Nested Loops (Double Loops)

📅 **Week 2**

### Concept Summary
A nested loop is a loop inside another loop. The **inner loop completes all its iterations** for each single iteration of the outer loop. Classic use cases: 2D matrix processing, Pythagorean triples. Key discipline: re-initialize inner variables at the **start of each outer iteration**.

### Key Syntax / Rules Box
```c
for (i = 0; i < m; i++) {         // Outer: rows
    rowsum = 0;                    // MUST reinitialize per row
    for (j = 0; j < n; j++) {     // Inner: columns
        scanf("%d", &a);
        if (i == j) trace += a;   // Diagonal: row index == col index
    }
}
```
- Total iterations = m × n (outer × inner).
- Variables shared between loops (e.g., `rowsum`) must be **reset** inside the outer loop.
- The inner loop's index (`j`) resets to its init value every time the outer loop body re-executes.

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int m, n, a, rowindex, colindex;
    int rowsum, rowsumsq, squaresum = 0;

    scanf("%d %d", &m, &n);   // Read matrix dimensions

    // Outer loop: iterate over rows
    rowindex = 0;
    while (rowindex < m) {
        rowsum = 0;            // CRITICAL: reset for each new row
        colindex = 0;

        // Inner loop: iterate over columns of this row
        while (colindex < n) {
            scanf("%d", &a);   // Read matrix element row-by-row
            rowsum = rowsum + a;
            colindex = colindex + 1;
        }
        // After inner loop: rowsum = sum of current row
        rowsumsq = rowsum * rowsum;  // Square of row sum
        squaresum = squaresum + rowsumsq;  // Accumulate
        rowindex = rowindex + 1;
    }
    printf("%d\n", squaresum);
    return 0;
}
```

**Sample input:**
```
2 3
1 0 -1
0 1 1
```
Row 0 sum = 1+0+(−1) = 0 → 0² = 0
Row 1 sum = 0+1+1 = 2 → 2² = 4
**Output: 4**

**What would NPTEL ask about this?**

❓ What happens if `rowsum = 0` is placed **before** the outer loop instead of inside it?
✅ The second row's sum gets **added to the first row's sum** — wrong answer.
💡 `rowsum` must be reset at the start of every outer iteration.

❓ For a 3×3 matrix, how many times does the `scanf` inside the inner loop execute?
✅ 9 times (3 outer × 3 inner).
💡 Total iterations of the inner body = m × n.

❓ In the trace problem, when is `i == j` true?
✅ Only for diagonal elements: (0,0), (1,1), (2,2), …
💡 This is the definition of the matrix diagonal. If indexing starts at 0, the diagonal spans (0,0) to (n-1,n-1).

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Not reinitializing `rowsum` each outer iteration | Previous row pollutes current row | `rowsum = 0;` inside outer loop |
| `i == j` written as `i = j` | Assignment, not comparison; always true or false | Use `==` |
| Wrong loop bound: `j < n` vs `j <= n` | Reads one extra or one fewer element | `j < n` (0-indexed, n elements) |
| Forgetting to `scanf` non-diagonal elements | Input buffer out of sync | Always read **all** matrix elements, even if you don't use them |

### Quick Recall
- Inner loop = n iterations per 1 outer iteration
- Total body executions = outer_count × inner_count
- Reinitialize inner accumulators **inside** outer loop
- Diagonal elements satisfy `row_index == col_index`

---

## 6. The `break` Statement & Infinite Loops

📅 **Week 2**

### Concept Summary
`while (1)` creates an **infinite loop** — the test is always true. The `break` statement provides a **controlled exit** from the **innermost** enclosing loop. When `break` executes inside a `for` loop, the **update expression is skipped** — control jumps directly out of the loop. `break` does NOT exit from an `if` statement.

### Key Syntax / Rules Box
```c
while (1) {         // Infinite loop — condition never false
    // ...
    if (condition)
        break;      // EXIT the innermost LOOP (not the if!)
    // ...
}
// Execution continues here after break
```
- `break` exits the **innermost** loop only (inner `for` inside outer `for` → only inner exits).
- In a `for` loop: `break` skips the **update expression**.
- In a `while` loop: `break` skips back to test (but since we're exiting, irrelevant).
- Equivalent to using a **flag variable** in the loop condition.

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int a, sum = 0;

    while (1) {              // Infinite loop — runs until break
        scanf("%d", &a);     // Read next number
        if (a == -1)
            break;           // Exit the while loop, NOT the if
        sum = sum + a;       // Only reached if a != -1
    }
    // Execution jumps here after break
    printf("Sum = %d\n", sum);
    return 0;
}
// Input: 5 3 2 -1  → Output: Sum = 10
```

**Break in a `for` loop — critical behaviour:**
```c
#include <stdio.h>
int main() {
    int i;
    for (i = 0; i < 10; i++) {   // Normal for loop
        if (i % 2 == 1)
            break;                // Break when i is odd
    }
    // After break, i is NOT updated (i++ did NOT run)
    printf("%d\n", i);            // Output: 1  (NOT 2!)
    return 0;
}
```

**What would NPTEL ask about this?**

❓ In the `for` loop above, why is the output `1` and not `2`?
✅ When `break` executes at i=1, control exits the loop **immediately** without running `i++`.
💡 The update expression in `for` is **skipped** when `break` fires. This is a top NPTEL trap.

❓ If there's a `for` loop inside a `while` loop and `break` is inside the `for` loop, which loop exits?
✅ Only the **inner** `for` loop exits.
💡 `break` always exits the **innermost** enclosing loop, not all loops.

❓ Does `break` exit an `if` statement?
✅ No — `break` exits the **loop**, even if the `break` is nested inside an `if` inside the loop.
💡 Work **outward** from the `break`: the first **loop** encountered is what exits.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Assuming `break` exits an `if` | Code after the if still executes | `break` exits loops (and `switch`), not `if` |
| Expecting `i++` to run before break | `i` retains its last value, not `i+1` | Remember: break skips update |
| Nested loops: wrong loop exits | Inner loop exits but outer keeps going | Put break in correct (outer) loop |
| `while(1)` with no `break` | Infinite loop — program hangs | Always have an exit condition |

### Quick Recall
- `break` → exits **innermost** loop immediately
- In `for`: **update is NOT executed** on break
- `break` does NOT exit `if`; it exits the surrounding **loop**
- `while (1)` = infinite loop; needs `break` or `return` to stop

---

## 7. The `continue` Statement

📅 **Week 2**

### Concept Summary
`continue` **skips the rest of the current iteration** and jumps to the next one. In a `while`/`do-while` it jumps to the **test expression**. In a `for` loop it jumps to the **update expression first**, then the test. Unlike `break`, `continue` does **not** exit the loop — it just skips to the next iteration. It is always replaceable by a nested `if`, but can make code cleaner.

### Key Syntax / Rules Box
```c
// In a for loop:
for (init; test; update) {
    if (skip_condition)
        continue;    // → jumps to UPDATE, then TEST
    // This code is skipped when continue executes
}

// In a while loop:
while (test) {
    if (skip_condition)
        continue;    // → jumps to TEST (no update to run)
    // This code is skipped
}
```
- `continue` in `for` → runs **update**, then **test**
- `continue` in `while` → runs **test** directly
- `continue` is equivalent to wrapping the remaining body in `if (!skip_condition)`

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int a, max = 0;

    // Read integers until non-digit; find max of positive numbers
    while (scanf("%d", &a) == 1) {  // scanf returns 1 on success
        if (a < 0)
            continue;   // Skip negatives — go back to while test
        if (max < a)    // Only reached for non-negative a
            max = a;
    }
    printf("Max = %d\n", max);
    return 0;
}
// Input: 1 -1 2 .   → Output: Max = 2
// Negative numbers are skipped; '.' causes scanf to return 0 → loop ends
```

**Equivalent code WITHOUT `continue`:**
```c
while (scanf("%d", &a) == 1) {
    if (a >= 0) {        // Extra level of nesting replaces continue
        if (max < a)
            max = a;
    }
}
```

**What would NPTEL ask about this?**

❓ In `for (i=0; i<5; i++) { if (i==2) continue; printf("%d ", i); }` what is printed?
✅ `0 1 3 4`
💡 When i=2: `continue` fires → jumps to `i++` (i becomes 3), then tests `3<5` → prints 3. The number 2 is skipped.

❓ What is the difference between `continue` in `for` vs `while`?
✅ In `for`: update runs before next test. In `while`: test runs immediately.
💡 This matters if the update has side effects. A `continue` in `while` that was supposed to be in `for` can cause an **infinite loop** if the update was supposed to break the condition.

❓ Can `continue` cause an infinite loop in `while`?
✅ Yes — if `continue` is hit before the variable controlling the test is updated.
💡 `while (i < 5) { if (...) continue; i++; }` → if the condition is always true, `i++` is never reached → infinite loop.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `continue` in `while` before update variable | Infinite loop | Ensure update is before `continue`, or use `for` |
| Confusing `continue` with `break` | `continue` doesn't exit the loop | `break` exits; `continue` skips to next iteration |
| Forgetting `continue` runs `update` in `for` | Miscount loop iterations | Remember: `for` → update runs on `continue` |

### Quick Recall
- `continue` = skip rest of body, go to next iteration
- `for` + `continue` → **update runs** (then test)
- `while` + `continue` → **test runs** directly (no update)
- Replaceable by: `if (!skip_condition) { rest of body }`

---

## 8. Flag Variables (Alternative to `break`/`continue`)

📅 **Week 2**

### Concept Summary
A **flag variable** is an integer variable (typically 0/1) that records whether a condition has occurred. Instead of using `break` inside a loop, you set the flag and put the condition in the loop header. This makes **all exit conditions visible** in the loop header without reading the body — improving readability at the cost of one extra variable.

### Key Syntax / Rules Box
```c
int flag = 0;                   // 0 = condition not yet met
for (i = 0; i < maxchar && flag == 0; i++) {
    // ...
    if (blank_line_detected)
        flag = 1;               // Signal the exit condition
}
// Two exit conditions visible in the for header: i >= maxchar OR flag == 1
```
- Flag is initialized to `0` (not met).
- Set to `1` when the condition is met.
- The loop condition checks `flag == 0` (continue only if NOT set).
- All exit conditions are **readable from the loop header** — no need to read the body.

### Detailed Code Example
```c
#include <stdio.h>
#define MAXCHAR 1000

int main() {
    int i, flag = 0;         // flag = 0: blank line not seen yet
    char current = '\n';     // Initialize to newline (important!)
    char previous;

    // Loop runs while: count < MAXCHAR AND no blank line seen
    for (i = 0; i < MAXCHAR && flag == 0; i++) {
        previous = current;           // Shift: prev ← current
        current = getchar();          // Read next character

        // Blank line = two consecutive newlines
        if (current == '\n' && previous == '\n')
            flag = 1;                 // Set flag instead of break
    }
    printf("\n");
    return 0;
}
```

**With `break` (equivalent, less readable):**
```c
for (i = 0; i < MAXCHAR; i++) {
    previous = current;
    current = getchar();
    if (current == '\n' && previous == '\n')
        break;            // Exit condition hidden inside body
}
```

**What would NPTEL ask about this?**

❓ Why is `current` initialized to `'\n'` before the loop?
✅ So the blank-line detection works from the very first character. If the user immediately presses Enter (blank line at the start), `previous = '\n'` and `current = '\n'` → blank line correctly detected.
💡 Without initialization, `previous` on the first iteration would be a garbage value.

❓ What are the two exit conditions for the flag-based for loop?
✅ (1) `i >= MAXCHAR` (max characters reached), (2) `flag == 1` (blank line detected).
💡 Both are visible in the `for` header — advantage over `break`.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Forgetting `flag = 0` init | Flag has garbage value; loop may not run | Always init flag to 0 |
| Checking `flag == 1` in body but not header | Loop continues past condition | Put `&& flag == 0` in header |
| Not initializing `current = '\n'` | Blank-line detection misses first line | Initialize before loop |

### Quick Recall
- Flag = integer variable: 0 = condition not met, 1 = met
- Advantage: exit conditions visible in loop **header**
- Disadvantage: one extra variable
- Prof. prefers `break`; flags preferred for **readability** of exit conditions

---

## 9. `scanf` Return Value & Input Termination

📅 **Week 2**

### Concept Summary
`scanf` **returns the number of items successfully read**. For `scanf("%d", &a)`, it returns `1` on success and `0` (or `EOF`) if it fails (e.g., encountering a non-digit like `.`). This return value is the standard C idiom for **input-driven loop termination** without a sentinel like -1.

### Key Syntax / Rules Box
```c
while (scanf("%d", &a) == 1) {
    // Execute body only when an integer was successfully read
}
// Loop ends when scanf fails (non-integer input or EOF)
```
- `scanf("%d", &a)` returns `1` → integer read successfully
- `scanf("%d", &a)` returns `0` → conversion failed (e.g., input is `.` or `a`)
- `scanf("%d", &a)` returns `EOF` (typically -1) → end of file
- Reading multiple values: `scanf("%d %d", &m, &n)` returns `2` on full success

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int a, max = 0;

    // Read positive integers; stop on any non-integer input
    while (scanf("%d", &a) == 1) {   // Returns 1 = int read OK
        if (a < 0)
            continue;                 // Skip negatives
        if (a > max)
            max = a;
    }
    // Loop exits when scanf returns 0 (e.g., input is ".")
    printf("Max positive: %d\n", max);
    return 0;
}
// Input: 1 -1 2 .   → Output: Max positive: 2
```

**What would NPTEL ask about this?**

❓ What does `scanf("%d", &a)` return when the next input character is `.`?
✅ `0` — the conversion failed; `a` is **unchanged**.
💡 `.` is not a valid integer, so `scanf` returns 0 (0 conversions succeeded).

❓ What does `scanf("%d %d", &m, &n)` return if only one integer is available before EOF?
✅ `1` — only one conversion succeeded.
💡 Use `== 2` to verify both were read; `== 1` means partial success.

❓ Can `scanf` return a negative value?
✅ Yes — it returns `EOF` (typically -1) on end-of-file before any conversion.
💡 `while (scanf(...) == 1)` handles both failure (returns 0) and EOF (returns -1) correctly by exiting.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Ignoring scanf return value | Loop runs on bad/no input; `a` = garbage | Check `scanf(...) == 1` |
| `while(scanf("%d",&a))` (checks non-zero) | `EOF = -1` is non-zero → loop keeps trying | Use `== 1` explicitly |
| Assuming `a` is updated on failed scan | `a` keeps its **previous** value | Always check return value |

### Quick Recall
- `scanf` returns the **count of items successfully converted**
- `== 1` for one integer, `== 2` for two, etc.
- Returns 0 on bad input, EOF on end-of-file
- Standard loop idiom: `while (scanf("%d", &a) == 1)`

---

## 10. GCD — Euclid's Algorithm (Case Study)

📅 **Week 1**

### Concept Summary
The **Euclidean GCD algorithm** uses the property: `GCD(a, b) = GCD(b, a % b)`. Repeatedly replace `(a, b)` with `(b, a % b)` until `b = 0`; at that point `a` is the GCD. This is dramatically faster than the naive approach of checking all divisors from n down to 1. Key programming insight: **three-variable sequential assignment** for the step `(a, b) → (b, a % b)`.

### Key Syntax / Rules Box
```c
// Core GCD step — requires temp variable g
g = a % b;   // Step 1: compute remainder
a = b;       // Step 2: old b becomes new a
b = g;       // Step 3: remainder becomes new b
// Repeat until b == 0; then a is the GCD
```
- Always ensure `a >= b` before starting (swap if needed).
- `GCD(a, 0) = a` for any a — this is the stopping condition.
- `%` = modulo (remainder). `a % b` gives remainder when a is divided by b.

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int a, b, g, t;

    scanf("%d %d", &a, &b);   // Read two integers

    // Ensure a >= b (swap if needed)
    if (a < b) {
        t = a; a = b; b = t;  // Classic 3-step swap
    }

    // Euclidean algorithm
    while (b != 0) {           // Stop when b = 0
        g = a % b;             // Compute remainder
        a = b;                 // Shift: a ← b
        b = g;                 // Shift: b ← remainder
    }
    // When loop exits, b = 0 and a = GCD
    printf("GCD = %d\n", a);
    return 0;
}
```

**Dry run for GCD(8, 6):**
| a | b | g = a%b | new a | new b |
|---|---|---------|-------|-------|
| 8 | 6 | 2       | 6     | 2     |
| 6 | 2 | 0       | 2     | 0     |

Loop exits: b=0, GCD = a = **2** ✓

**Dry run for GCD(102, 21):**
| a   | b  | g = a%b |
|-----|----|---------|
| 102 | 21 | 18      |
| 21  | 18 | 3       |
| 18  | 3  | 0       |

GCD = **3** ✓

**What would NPTEL ask about this?**

❓ What happens if the order is `b = g; a = b;` instead of `a = b; b = g;`?
✅ Both become `g` (the remainder) — wrong! The original `b` value is lost.
💡 Sequence matters. You must save `b`'s value in `a` **before** overwriting `b`.

❓ What is GCD(5, 0)?
✅ 5 — because the loop condition `b != 0` is immediately false; `a` is returned as-is.
💡 `GCD(n, 0) = n` by definition; the algorithm handles this correctly.

❓ Why must a ≥ b at the start?
✅ If a < b, then `a % b = a` (remainder of a smaller number divided by larger = the number itself). The algorithm still works, but one step is wasted. Swapping first is cleaner.
💡 Actually the algorithm self-corrects after one step even without the swap — but NPTEL may ask you to trace without the swap.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Wrong order: `b=g; a=b;` | Both become g | `a=b; b=g;` |
| Not swapping when a < b | Extra first step (but algorithm is still correct) | Swap for efficiency |
| Using `-` (subtraction) instead of `%` | Very slow (Euclid's original, not modular version) | Use `%` |
| Stopping when `a == 0` instead of `b == 0` | Wrong GCD | Stop when `b == 0`, return `a` |

### Quick Recall
- `GCD(a, b) = GCD(b, a % b)` until b = 0
- Answer is `a` when loop exits (`b = 0`)
- Swap needs temp: `t = a; a = b; b = t;`
- `%` = remainder operator in C

---

## 11. Matrix Trace (Nested `for` Loop Case Study)

📅 **Week 2**

### Concept Summary
The **trace** of a matrix is the sum of **diagonal elements** — elements where `row_index == col_index`. Implemented with a nested `for` loop: the outer loop iterates rows, the inner loop iterates columns. **All** elements must be `scanf`'d even if only diagonal elements are used (to keep the input buffer in sync).

### Key Syntax / Rules Box
```c
for (i = 0; i < n; i++) {        // row index
    for (j = 0; j < n; j++) {    // column index
        scanf("%d", &a);          // ALWAYS read; even non-diagonal
        if (i == j)               // Diagonal: row == col
            trace += a;           // Add to trace
    }
}
```
- C arrays/indices are **0-based**: first row = row 0, last row = row n-1.
- Diagonal condition: `i == j` (NOT `i = j`).
- Omitting `scanf` for non-diagonal elements **corrupts input stream**.

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int n, i, j, a, trace = 0;

    scanf("%d", &n);           // n × n matrix

    for (i = 0; i < n; i++) {        // Outer: row 0 to n-1
        for (j = 0; j < n; j++) {    // Inner: col 0 to n-1
            scanf("%d", &a);          // Read element (i, j)
            if (i == j)               // Is it on the diagonal?
                trace = trace + a;    // Add to trace
        }
    }
    printf("Trace = %d\n", trace);
    return 0;
}
```
**Input:**
```
3
1 2 3
1 3 3
-1 0 -1
```
Diagonal elements: a[0][0]=1, a[1][1]=3, a[2][2]=-1 → Trace = **3**

**What would NPTEL ask about this?**

❓ For a 3×3 matrix, how many total `scanf` calls execute?
✅ 9 (3 rows × 3 columns)
💡 Even non-diagonal elements must be read to advance the input. Skipping them = reading wrong values for later cells.

❓ What if the diagonal condition is `if (i = j)` instead of `if (i == j)`?
✅ This is an **assignment** not a comparison. `i = j` assigns j's value to i and the result (j's value) is the condition. If j ≠ 0, it's truthy → most elements added to trace (wrong).
💡 Classic `=` vs `==` bug — a guaranteed NPTEL question.

❓ What is `a[2][2]` in a 3×3 0-indexed matrix?
✅ The element in the 3rd row, 3rd column (the bottom-right element).
💡 0-indexing: rows 0,1,2 and cols 0,1,2. `a[2][2]` = last diagonal element.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `if (i = j)` | Assignment, not comparison; wrong elements added | `if (i == j)` |
| Skipping scanf for non-diagonal | Input stream offset; all subsequent reads are wrong | Always scanf all elements |
| `trace` not initialized to 0 | Garbage starting value | `int trace = 0;` |
| Loop bound `i <= n` | Reads n+1 rows (one extra, undefined input) | `i < n` |

### Quick Recall
- Trace = sum of diagonal elements where `row == col`
- Always read **all** elements even if not using them
- 0-indexed: `i` and `j` go 0 to n-1
- `if (i == j)` — double equals!

---

## 12. Pythagorean Triples (Multi-variable `continue` Case Study)

📅 **Week 2**

### Concept Summary
Finding consecutive Pythagorean triples in a stream requires maintaining a **sliding window of three variables**: `pp` (previous-to-previous), `prev` (previous), `curr` (current). Negative numbers are skipped using `continue`. A `count` variable tracks how many positive numbers have been seen so far, to ensure we have enough context.

### Key Syntax / Rules Box
```c
// Sliding window of 3 positive numbers:
// pp = a, prev = b, curr = c
// Check: pp*pp + prev*prev == curr*curr
if (pp*pp + prev*prev == curr*curr)
    printf("%d %d %d\n", pp, prev, curr);
// Advance window:
pp = prev;
prev = curr;
// curr = next positive number (from next loop iteration)
```
- Negative/zero numbers → `continue` (skip, don't update the triple)
- Need at least 3 positive numbers before first check
- After a triple is found, **advance pp and prev** (curr becomes next positive number)

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int n, i, curr, prev, pp;
    int count = 0;  // Count of positive numbers seen so far

    scanf("%d", &n);  // n = total numbers to process

    for (i = 0; i < n; i++) {
        scanf("%d", &curr);       // Read next number

        if (curr <= 0)
            continue;             // Skip non-positive: jump to i++, then test

        // curr is positive — update sliding window
        if (count == 0) {
            pp = curr;            // First positive: init pp
            count = 1;
        } else if (count == 1) {
            prev = curr;          // Second positive: init prev
            count = 2;
        } else {
            // Have pp, prev, curr — check Pythagorean triple
            if (pp*pp + prev*prev == curr*curr)
                printf("%d %d %d\n", pp, prev, curr);
            // Slide window: pp ← prev, prev ← curr
            pp = prev;
            prev = curr;
            // count stays at 2 (convention: >= 2 means we have context)
        }
    }
    return 0;
}
```
**Input:** `8  3 -3 -4 -5 4 5 6 7`
Positive numbers in order: 3, 4, 5, 6, 7
- (3,4,5): 9+16=25=25 ✓ → print `3 4 5`
- (4,5,6): 16+25=41 ≠ 36 → no
- (5,6,7): 25+36=61 ≠ 49 → no

**What would NPTEL ask about this?**

❓ What does `continue` do when `curr <= 0` inside a `for` loop?
✅ Skips the rest of the body, runs `i++`, then checks `i < n`.
💡 The sliding window variables (`pp`, `prev`) are NOT updated for skipped numbers.

❓ Why is `count` needed?
✅ To avoid checking a triple before we have 3 valid positive numbers. Without it, `pp` and `prev` are uninitialized garbage.
💡 On the first positive number, we only have one value. We need at least 3.

❓ If `pp*pp + prev*prev == curr*curr` uses integer arithmetic and pp=3,prev=4,curr=5, what is the result?
✅ `9 + 16 == 25` → `25 == 25` → `1` (true) → triple is printed.
💡 Integer multiplication: `3*3 = 9`, `4*4 = 16`, `5*5 = 25`. Perfect squares, no overflow for small values.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Not using `continue` for negatives | Negatives pollute the sliding window | `if (curr <= 0) continue;` |
| Not re-initializing pp/prev on first 1-2 positives | Uninitialized garbage in triple check | Use `count` to gate the check |
| Advancing window before printing | Wrong triple printed | Print first, then slide |
| `pp*pp + prev*prev = curr*curr` | Assignment in condition | Use `==` |

### Quick Recall
- Sliding window: pp, prev, curr (3 variables)
- Skip negatives with `continue`
- Count positive numbers seen; only check when count ≥ 3 (i.e., else branch)
- Check: `pp² + prev² == curr²`

---

## 13. `getchar` vs `scanf %c` for Characters

📅 **Week 2**

### Concept Summary
`getchar()` reads **one character at a time** from standard input, including whitespace and newlines. It is essentially equivalent to `scanf("%c", &ch)`. Both return the character read. `getchar` is commonly used when character-by-character processing is needed (e.g., detecting blank lines). Detecting a **blank line** requires remembering the **previous** character.

### Key Syntax / Rules Box
```c
char current, previous;
current = '\n';           // Initialize to newline before loop

// Inside loop:
previous = current;       // Shift
current = getchar();      // Read next character (includes '\n')
// OR equivalently:
// scanf("%c", &current);

// Blank line detection:
if (current == '\n' && previous == '\n')
    // Blank line found!
```
- `'\n'` = newline character literal
- A **blank line** = two consecutive `'\n'` characters
- `getchar()` reads whitespace (including `'\n'`); `scanf("%d")` skips whitespace
- Pre-initializing `current = '\n'` allows detecting a blank first line

### Detailed Code Example
```c
#include <stdio.h>
#define MAXCHAR 1000

int main() {
    int i;
    char current = '\n';  // Pre-init: treats "start" as after a newline
    char previous;

    for (i = 0; i < MAXCHAR; i++) {
        previous = current;          // Remember last char
        current = getchar();         // Read one char (incl. '\n')

        if (current == '\n' && previous == '\n') {
            break;   // Two consecutive newlines = blank line
        }
    }
    printf("\n");
    return 0;
}
```

**What would NPTEL ask about this?**

❓ Why is `current` initialized to `'\n'` before the loop?
✅ So that if the user immediately enters a blank line (presses Enter twice from the start), the condition `current == '\n' && previous == '\n'` triggers correctly on the **first** iteration.
💡 If initialized to `'\0'` or garbage, the first blank-line check would be wrong.

❓ Does `scanf("%d", &a)` read newline characters?
✅ No — `scanf` with `%d` **skips** leading whitespace (spaces, tabs, newlines) before reading.
💡 `getchar()` / `scanf("%c")` reads **everything** including whitespace.

❓ What character does `getchar()` return when the user presses Enter?
✅ `'\n'` (newline character, ASCII 10)
💡 Every time Enter is pressed, a `'\n'` goes into the input stream.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Not pre-initializing `current` | First blank line may not be detected | `char current = '\n';` |
| Using `scanf("%d")` to read chars | Newlines skipped; can't detect blank lines | Use `getchar()` or `scanf("%c")` |
| `current == "\n"` (double quotes) | Comparing char to string pointer (type error) | `current == '\n'` (single quotes) |

### Quick Recall
- `getchar()` ≈ `scanf("%c", &ch)` — reads **everything** including whitespace
- `'\n'` = newline (single quotes for char literals)
- Blank line = two consecutive `'\n'`
- Pre-init `current = '\n'` to handle blank first line

---

## 14. The Comma Operator in `for` Loops

📅 **Week 2**

### Concept Summary
The **comma operator** in C evaluates expressions left-to-right and returns the value of the last one. Inside a `for` loop's **init expression**, it allows initializing multiple variables in one statement. This reduces lines of code and is idiomatic C.

### Key Syntax / Rules Box
```c
// Initialize two variables in one for-loop init:
for (sum = 0, i = 0; i < m; i++) {
    // ...
}
// Equivalent to:
sum = 0;
for (i = 0; i < m; i++) { ... }
```
- Comma in `for` init: evaluates **left to right** (`sum=0` first, then `i=0`)
- Both `sum` and `i` are initialized before the first test
- The comma operator can also appear in the update expression: `i++, j--`

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int m, i, a, sum;

    scanf("%d", &m);          // Read count

    // Comma operator initializes both sum and i at once
    for (sum = 0, i = 0; i < m; i++) {
        scanf("%d", &a);
        sum = sum + a;
    }
    printf("Sum = %d\n", sum);
    return 0;
}
```

**What would NPTEL ask about this?**

❓ In `for (sum = 0, i = 1; i <= 5; i++)`, what is `sum`'s initial value?
✅ `0` — the comma operator evaluates left to right; `sum = 0` runs first.
💡 Both assignments happen before the test `i <= 5` is first evaluated.

❓ Is `for (sum = 0, i = 0; ...)` equivalent to `sum = 0; for (i = 0; ...)`?
✅ Yes — functionally identical. The comma operator in init is syntactic sugar.
💡 Prefer whichever is clearer; NPTEL may ask you to identify equivalence.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `int sum = 0, i = 0` inside for | Declaration inside `for` init (C99+ only, not C89) | Declare before `for`; init with comma operator |
| Confusing `,` operator with `,` in declarations | Different contexts — comma in `for` init is the operator | Know the context |

### Quick Recall
- `for (a=0, b=1; ...; ...)` — init multiple vars with comma
- Left-to-right evaluation
- Purely syntactic convenience — no functional difference from separate init

---

---

## 15. `if` and `if-else` Statements

📅 **Week 1**

### Concept Summary
The `if` statement executes a block only when a condition is true. The `if-else` adds an alternative branch for when the condition is false. In C, `0` = false and **any non-zero value = true**. `if-else` chains (`else if`) test multiple conditions in sequence — only the **first true branch** executes.

### Key Syntax / Rules Box
```c
// Simple if
if (condition)
    statement;          // No braces needed for single statement

// if-else
if (condition)
    statement_true;
else
    statement_false;

// if-else if-else chain
if (condition1)
    statement1;
else if (condition2)
    statement2;
else
    statement_default;
```
- Condition evaluates to **int**: 0 = false, non-zero = true
- `else` always binds to the **nearest preceding unmatched `if`**
- Braces `{}` optional for single statements; **always use braces** for clarity
- `=` inside condition is a common bug: `if (a = 5)` always true

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int a;
    scanf("%d", &a);

    if (a % 6 == 0)                         // Divisible by 6?
        printf("%d is divisible by 6\n", a);
    else if (a % 3 == 0)                    // Else: divisible by 3?
        printf("%d is divisible by 3 only\n", a);
    else if (a % 2 == 0)                    // Else: divisible by 2?
        printf("%d is divisible by 2 only\n", a);
    else
        printf("%d is not divisible by 2 or 3\n", a);

    return 0;
}
```

**What would NPTEL ask about this?**

❓ For `a = 12`, which branch executes?
✅ The first: `12 % 6 == 0` → prints "divisible by 6". The other branches are skipped.
💡 In an `else if` chain, only the **first true** condition executes. Even though 12 is also divisible by 3 and 2, those branches are never reached.

❓ What is the output for `a = 9`?
✅ "9 is divisible by 3 only" — `9 % 6 = 3 ≠ 0`, but `9 % 3 = 0`.
💡 The `else if` is only checked when the `if` above it is false.

❓ What is the difference between `if (a = 5)` and `if (a == 5)`?
✅ `a = 5` assigns 5 to a (always true since 5 ≠ 0). `a == 5` tests if a equals 5.
💡 Classic `=` vs `==` trap — one of the most common C bugs.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `if (a = 5)` | Assignment; always true | `if (a == 5)` |
| `if (a == 5);` (semicolon after condition) | Empty if body; next line always runs | Remove the `;` |
| `else` without preceding `if` | Compile error | Match every `else` to an `if` |
| Testing float equality: `if (f == 3.14)` | Unreliable due to float precision | Use range: `if (f > 3.13 && f < 3.15)` |

### Quick Recall
- `0` = false, non-zero = true in C
- `else` binds to nearest unmatched `if`
- `else if` chains: only first true branch runs
- `=` assigns; `==` compares — never mix them in conditions

---

## 16. Operators — Modulo, Logical AND/OR/NOT, Leap Year

📅 **Week 1**

### Concept Summary
The **modulo operator `%`** gives the remainder of integer division — the primary tool for divisibility checks. **Logical operators** (`&&`, `||`, `!`) combine or negate boolean conditions, enabling complex decision-making in a single `if` statement. **Short-circuit evaluation** means the second operand is skipped when the result is already determined.

### Key Syntax / Rules Box
```c
a % b       // Remainder when a is divided by b; result = 0 means a divisible by b
&&          // Logical AND: true only if BOTH operands are non-zero
||          // Logical OR: true if AT LEAST ONE operand is non-zero
!           // Logical NOT (unary): flips truth value; !0 = 1, !non-zero = 0
```
- All logical operators return **int**: `1` (true) or `0` (false)
- `&&` short-circuits: if left is `0`, right is **not evaluated**
- `||` short-circuits: if left is non-zero, right is **not evaluated**
- `!` is **unary** (one operand); `&&` and `||` are **binary** (two operands)

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int year;
    scanf("%d", &year);

    // Leap year: divisible by 4 AND (not by 100 OR divisible by 400)
    if ((year % 4 == 0) && ((year % 100 != 0) || (year % 400 == 0)))
        printf("%d is a leap year.\n", year);
    else
        printf("%d is not a leap year.\n", year);

    return 0;
}
```

**Leap Year Logic Breakdown:**
| Condition | Meaning |
|-----------|---------|
| `year % 4 == 0` | Must be divisible by 4 |
| `year % 100 != 0` | But NOT by 100 |
| `year % 400 == 0` | UNLESS also divisible by 400 |

**Dry Run:**
| Year | %4 | %100 | %400 | Leap? |
|------|----|------|------|-------|
| 2000 | 0 | 0 | 0 | ✅ Yes (400) |
| 1900 | 0 | 0 | ≠0 | ❌ No (100, not 400) |
| 2024 | 0 | ≠0 | ≠0 | ✅ Yes (4, not 100) |
| 2023 | ≠0 | — | — | ❌ No |

**What would NPTEL ask about this?**

❓ What does `!` do in `if (!(a % 3 == 0))`?
✅ Negates: checks if a is **not** divisible by 3. Same as `a % 3 != 0`.
💡 `!(a % 3 == 0)` → `!true` → `false` when divisible. Equivalent to `a % 3 != 0`.

❓ In `if (a && b)`, if `a = 0`, is `b` evaluated?
✅ No — short-circuit: `0 && anything = 0`, so `b` is never evaluated.
💡 Prevents side-effects and potential errors from evaluating `b` unnecessarily.

❓ What is `5 % 3`? What is `3 % 5`?
✅ `5 % 3 = 2`; `3 % 5 = 3` (when dividend < divisor, remainder = dividend)
💡 `a % b = a` when `a < b`.

❓ What is `!(0)` and `!(5)`?
✅ `!(0) = 1`; `!(5) = 0`. NOT flips 0↔non-zero.
💡 `!` always returns exactly `0` or `1`, never the original value.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `&` instead of `&&` | Bitwise AND, not logical | Use `&&` for logical conditions |
| `\|` instead of `\|\|` | Bitwise OR, not logical | Use `\|\|` for logical conditions |
| `!(a % 3)` without `== 0` | Works: `a%3=0` → `!0=1` (true). But obscure | Prefer explicit: `a % 3 == 0` |
| Forgetting parentheses in leap year | Wrong precedence | Always parenthesize complex conditions |

### Quick Recall
- `a % b == 0` → b divides a exactly
- `&&` = AND (both must be true); `||` = OR (either must be true); `!` = NOT
- Short-circuit: `&&` stops at first false; `||` stops at first true
- Leap year: `(% 4 == 0) && ((% 100 != 0) || (% 400 == 0))`
- All logical results are `0` or `1` (int)

---

## 17. Variables & Data Types — `int`, `float`, Format Specifiers

📅 **Week 1**

### Concept Summary
Every variable in C must be **declared** with a type before use. **`int`** stores whole numbers; **`float`** stores real (decimal) numbers with finite precision. The **assignment operator `=`** copies the right-hand value into the left-hand variable — it is NOT mathematical equality. Format specifiers (`%d`, `%f`) tell `printf`/`scanf` how to interpret data.

### Key Syntax / Rules Box
```c
int a;              // Integer: whole numbers (no decimal)
float b;            // Float: real numbers (decimal, limited precision)

a = 10;             // Assignment: store 10 in a
b = 3.14;           // Store 3.14 in b

printf("%d", a);    // %d prints int
printf("%f", b);    // %f prints float (default 6 decimal places)
scanf("%d", &a);    // Read int from input
scanf("%f", &b);    // Read float from input
```
- Variable names: letters, digits, `_` only; **cannot start with a digit**
- C is **case-sensitive**: `Temp` ≠ `temp` ≠ `TEMP`
- `float` is a **machine approximation** of real numbers — limited precision
- Format specifiers: `%d` (int), `%f` (float), `%lf` (double in scanf), `%c` (char)

### Detailed Code Example — Celsius to Fahrenheit
```c
#include <stdio.h>
int main() {
    float centigrade;    // Box for real number (Celsius input)
    float fahrenheit;    // Box for result

    centigrade = 50;     // Store 50 (converted to 50.0 since type is float)

    // Formula: F = 9*C/5 + 32
    // Must write 9*centigrade explicitly — C doesn't infer multiplication
    fahrenheit = 9 * centigrade / 5 + 32;

    printf("%f Celsius = %f Fahrenheit\n", centigrade, fahrenheit);
    // Output: 50.000000 Celsius = 122.000000 Fahrenheit
    return 0;
}
```

**What would NPTEL ask about this?**

❓ What does `int b = 3; int a = 2; a = b;` leave in `a` and `b`?
✅ Both `a = 3`, `b = 3`. Assignment copies the value — `b` is unchanged.
💡 `a = b` means "copy b's value into a". If b changes later, a does NOT change automatically.

❓ What is the output of `printf("%d", 3.14)`?
✅ Undefined behaviour — `%d` expects an int, but 3.14 is a float. Garbage output.
💡 Always match format specifier to variable type.

❓ Why is `float` used instead of `int` for temperature conversion?
✅ Because `9/5 = 1` (integer division), losing the `.8`. Float preserves the decimal: `9.0/5 = 1.8`.
💡 `9 * 50 / 5 = 450 / 5 = 90` (int math, correct here), but `7 / 2 = 3` not 3.5 — use `float` for accuracy.

❓ What does `centigrade = 50;` actually store since `centigrade` is `float`?
✅ `50.000000` — the integer 50 is automatically converted to float `50.0`.
💡 C performs implicit type conversion when assigning int to float.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `int a; printf("%f", a)` | Wrong format; garbage output | Match type: `float a; printf("%f", a)` |
| `float f; scanf("%d", &f)` | Wrong specifier; garbage value | Use `scanf("%f", &f)` |
| Variable name starting with digit: `1count` | Compile error | `count1` or `count` |
| `CENTIGRADE` when declared as `centigrade` | Undeclared variable error | Exact case must match |
| `fahrenheit = 9/5 * c + 32` | `9/5 = 1` (int division) | `fahrenheit = 9.0/5 * c + 32` |

### Quick Recall
- `int` = whole numbers; `float` = decimal numbers
- `=` in C is assignment (copy), NOT mathematical equality
- `%d` → int, `%f` → float, `%c` → char, `%lf` → double (scanf)
- Variable names: case-sensitive, no starting digit, only letters/digits/underscore
- `float` has limited precision — approximation of real numbers

---

## 18. Tracing Programs — `printf`, `\n`, Comments

📅 **Week 1**

### Concept Summary
**Tracing** means following a program's execution line-by-line, tracking what each statement does. Statements execute **top to bottom** sequentially. `printf` outputs to terminal. The **newline character `\n`** moves output to the next line. **Comments** (`/* ... */` or `//`) are ignored by the compiler but vital for readability.

### Key Syntax / Rules Box
```c
/* Multi-line comment — ignored by compiler */
// Single-line comment (C99+)

printf("hello");          // Prints: hello (cursor stays on same line)
printf("hello\n");        // Prints: hello (cursor moves to next line)
printf("a\nb\nc\n");      // Prints:
                          //   a
                          //   b
                          //   c
```
- `\n` = **newline** (backslash + n = ONE character, ASCII 10)
- `\n` vs `/n`: backslash `\`, NOT forward slash `/`
- Two consecutive `printf` statements print on the **same line** by default
- `#include <stdio.h>` must be present for `printf` to work
- `/* */` comments can span multiple lines; `//` comments end at line break

### Detailed Code Example
```c
#include <stdio.h>

/* This is a simple C program demonstrating printf and \n */
int main() {
    printf("welcome to");          // No \n → stays on same line
    printf("C programming");       // Prints right after "welcome to"
    // Output: welcome toC programming  (no space between!)

    printf("\n");                  // Moves to new line

    printf("Line 1\n");            // Prints then newline
    printf("Line 2\n");            // Prints on new line
    // Output:
    // Line 1
    // Line 2

    printf("A\n\nB\n");           // Double \n creates blank line
    // Output:
    // A
    //          ← blank line
    // B

    return 0;
}
```

**What would NPTEL ask about this?**

❓ What is the output of `printf("welcome to"); printf("C programming");`?
✅ `welcome toC programming` — all on one line, no space.
💡 `printf` does NOT add spaces or newlines automatically between calls.

❓ How many characters is `\n`?
✅ **One** — it's a single special character (escape sequence), despite being written as two letters.
💡 `\n` = newline; `\t` = tab; `\\` = backslash. All count as one character each.

❓ What does `printf("A\n\nB\n")` output?
✅ `A`, blank line, `B`, then cursor to next line.
💡 The two `\n\n` creates one newline (end of A's line) plus one blank line.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `/n` instead of `\n` | Prints `/n` literally — no newline | Use backslash `\n` |
| Unclosed `"` in printf | Compile error | Close all string literals |
| Forgetting `;` after printf | Compile error | Every statement ends with `;` |
| Comment inside string: `printf("/* hi */")` | Prints `/* hi */` literally | Comments outside strings only |

### Quick Recall
- Statements execute **top to bottom**, one at a time
- `printf` keeps cursor on same line unless `\n` is included
- `\n` = newline (one character, backslash-n)
- Comments: `/* ... */` (multi-line) or `//` (single-line, C99+)
- Compiler **ignores** comments — they are for humans only

---

## 19. `while` Loop — Structure, Sentinel Pattern, Priming Read

📅 **Week 2**

### Concept Summary
The `while` loop executes its body **as long as the condition is true** (non-zero). Unlike `for`, it is preferred when the number of iterations is **not known in advance** — e.g., reading until a sentinel value. A **priming read** (reading one value before the loop) is a common idiom: it gives the condition something to test on the first check.

### Key Syntax / Rules Box
```c
while (expression) {
    // body — executes as long as expression is non-zero
}
// Flowchart: test → (true) body → test → ... → (false) exit
```
- `expression` is evaluated **before** each iteration (including the first)
- If expression is false from the start → body **never executes**
- Something inside the body must eventually make expression false → avoid infinite loops
- Non-zero = true; zero = false (C convention)
- `while` vs `if`: `while` loops back to test; `if` does not

### Detailed Code Example — Sum Until Sentinel
```c
#include <stdio.h>
int main() {
    int a, s;

    s = 0;              // Initialize sum BEFORE the loop
    scanf("%d", &a);    // PRIMING READ: read first number before loop

    while (a != -1) {   // Test: continue until sentinel -1
        s = s + a;      // Add current number to sum
        scanf("%d", &a);// Read NEXT number (updates condition variable!)
    }
    // Loop exits: a == -1, but -1 is NOT added to sum
    printf("Sum = %d\n", s);
    return 0;
}
// Input: 4 15 -5 -1  →  Output: Sum = 14
```

**Trace for input `4, 15, -5, -1`:**
| State | a | s | Condition |
|-------|---|---|-----------|
| After priming read | 4 | 0 | 4 ≠ -1 → enter |
| After iteration 1 | 15 | 4 | 15 ≠ -1 → enter |
| After iteration 2 | -5 | 19 | -5 ≠ -1 → enter |
| After iteration 3 | -1 | 14 | -1 ≠ -1 → **false, exit** |

**Output: 14** ✓ (-1 not included)

**What would NPTEL ask about this?**

❓ How many iterations does the loop execute for input `4, 15, -5, -1`?
✅ **3** — the loop body runs for 4, 15, and -5. When -1 is read, the condition fails; the body is **not entered**.
💡 Number of iterations ≠ number of inputs. The sentinel is read but never processed.

❓ What happens if `s = 0` is placed **after** the priming read instead of before?
✅ The result is the same here — but good practice is to initialize before the priming read in case initialization depends on the first read.
💡 Always initialize accumulators before the loop for clarity.

❓ What if the priming read is removed and `scanf` is only inside the loop?
✅ The while condition has an **uninitialized** `a` — undefined behaviour; the loop may never execute or run garbage.
💡 The priming read pattern ensures the condition variable has a valid value before the first test.

### Loop Invariant for Summation
> **Invariant:** At the start of each iteration, `s` holds the sum of all numbers read **so far, except the current value in `a`.**
> - Before iteration 1: s=0, a=4 → s = sum of zero numbers ✓
> - At termination: a=-1, s=sum of all valid numbers ✓ (sentinel excluded)

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| No priming read | `a` uninitialized; UB | Read first value before `while` |
| `s` uninitialized | Garbage starting sum | `s = 0` before loop |
| `scanf` only before loop, not inside | `a` never changes; infinite loop | `scanf` at **end** of loop body |
| `while (a = -1)` | Assignment; always -1 (truthy → infinite loop) | `while (a != -1)` |

### Quick Recall
- `while (condition)` — test first, then body
- Body executes **0 or more** times
- Priming read: read once before loop to initialize condition variable
- Re-read at **end** of loop body to update condition variable
- Sentinel: special value signaling end of input; NOT added to result

---

## 20. Loop Invariants

📅 **Week 2**

### Concept Summary
A **loop invariant** is a property that holds **before every iteration** of a loop and **after the loop terminates**. It is used to **prove correctness** — if the invariant holds at termination and the loop stops at the right condition, the final result must be correct. Loop invariants are a formal reasoning tool, not executable code.

### Key Syntax / Rules Box
```
Loop Invariant = property true at START of each iteration

To prove a loop is correct:
1. Define the invariant
2. Verify it holds BEFORE the first iteration (initialization)
3. Verify it's maintained AFTER each iteration (preservation)
4. At termination: invariant + loop condition being false → correct answer
```

### Two Key Examples

**Example 1: Sum Until Sentinel (-1)**
> **Invariant:** `s` = sum of all values read **except** the current value in `a`
> - Init: `s=0`, `a=first_number` → s = sum of empty set = 0 ✓
> - Preservation: loop adds `a` to `s`, reads new `a` → invariant holds for new `a` ✓
> - Termination: `a == -1` → `s` = sum of all values except -1 ✓

**Example 2: GCD (Euclidean Algorithm)**
> **Invariant:** `GCD(original_A, original_B) = GCD(current_a, current_b)`
> - Init: `a,b = input values` → GCD(A,B) = GCD(a,b) ✓
> - Preservation: transform `(a,b) → (b, a%b)`. Since GCD(x,y) = GCD(y, x%y), invariant maintained ✓
> - Termination: `b == 0` → GCD(a,0) = a → correct answer ✓

**What would NPTEL ask about this?**

❓ What is a loop invariant?
✅ A property/condition that is **true at the start of every iteration** and at loop termination.
💡 Used to formally prove correctness of loops without running them.

❓ For the GCD while loop, what is the invariant?
✅ `GCD(A, B) = GCD(a, b)` — GCD of original inputs equals GCD of current a and b at every step.
💡 This invariant plus `b=0` at termination proves `a = GCD(A,B)`.

### Quick Recall
- Loop invariant = property true before every iteration
- Three steps: init → preservation → termination
- Invariant at termination + stopping condition → proves correctness
- GCD invariant: `GCD(A,B) = GCD(a,b)` throughout
- Sum invariant: `s` = sum of all processed values except current `a`

---

## 21. `do-while` Loop

📅 **Week 2**

### Concept Summary
The `do-while` loop is a variant where the **body executes first, then the condition is tested**. This guarantees **at least one execution** of the body — unlike `while` which may execute zero times. It is **equally expressive** as `while` (any `do-while` can be rewritten as `while`), but produces cleaner code when an initial action is mandatory.

### Key Syntax / Rules Box
```c
do {
    // body — executes at LEAST once
} while (expression);   // ← SEMICOLON required here!

// Equivalent while:
body;                   // Execute body once before loop
while (expression) {
    body;               // Execute body in loop
}
```
- **Critical:** Semicolon after `while (expression)` is **mandatory** — forgetting it is a compile error
- Body always runs at least once — even if expression is false from the start
- `do-while` and `while` are equally powerful; choice depends on which is more natural

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int a;

    // Print numbers including the sentinel -1
    // With while: needs priming read + extra printf after loop
    // With do-while: cleaner!
    do {
        scanf("%d", &a);   // Read number (always reads at least once)
        printf("%d\n", a); // Print (prints even if a == -1)
    } while (a != -1);    // Stop after printing -1

    return 0;
}
// Input: 5 3 -1
// Output: 5
//         3
//         -1
```

**Comparison — while vs do-while for same problem:**
```c
// WHILE version (needs extra printf after loop):
scanf("%d", &a);        // priming read
while (a != -1) {
    printf("%d\n", a);
    scanf("%d", &a);
}
printf("%d\n", a);      // Must print -1 separately!

// DO-WHILE version (cleaner — no extra printf needed):
do {
    scanf("%d", &a);
    printf("%d\n", a);  // Prints -1 naturally at the end
} while (a != -1);
```

**What would NPTEL ask about this?**

❓ How many times does a `do-while` body execute if the condition is false from the very first check?
✅ **Once** — the body always executes before the first condition check.
💡 This is the fundamental difference from `while` (which may execute 0 times).

❓ What is the compile error if you write `do { ... } while (a != -1)` without the semicolon?
✅ Syntax error — the semicolon after `while (expression)` is mandatory in `do-while`.
💡 Contrast with `while (condition) { }` — NO semicolon after the while condition there.

❓ Can every `do-while` loop be rewritten as a `while` loop?
✅ Yes — just execute the body once before the `while` condition.
💡 They are equally expressive; choice is stylistic based on clarity.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Missing `;` after `while(expr)` in do-while | Compile error | `} while (expr);` |
| Using `while` when body must run at least once | Body skipped if condition initially false | Use `do-while` |
| Semicolon after `while(cond)` in plain while | Empty loop body; infinite loop or logic error | `while (cond) {` no semicolon |

### Quick Recall
- `do { body } while (condition);` — body runs **at least once**
- **Semicolon after `while(...)`** is mandatory — most common mistake
- Equally expressive as `while`; choose for clarity
- Best for: sentinel must be processed, menu must display before input, input validation

---

## 22. Longest Contiguous Increasing Subsequence (LCIS)

📅 **Week 2**

### Concept Summary
Given a stream of numbers ending with `-1`, find the **length of the longest contiguous increasing subsequence** — a run of consecutive numbers where each is **strictly greater** than the previous. Uses a **sliding window** of `previous` and `current`, with two counters: `len` (current streak) and `maxlen` (best streak seen). **Critical edge case:** if the longest run is the **last** one, it must be compared after the loop.

### Key Syntax / Rules Box
```c
// Core variables:
int p;          // previous number
int c;          // current number
int len;        // length of current increasing streak
int maxlen;     // maximum streak length seen so far

// Core decision:
if (p < c)      len++;              // Extend streak
else {          
    if (len > maxlen) maxlen = len; // Save if streak beats record
    len = 1;                        // Reset for new streak
}
p = c;          // Slide window: current becomes previous

// CRITICAL post-loop check:
if (len > maxlen) maxlen = len;     // Handle case: longest at end
```

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int p, c, len = 0, maxlen = 0;

    // Read first number
    scanf("%d", &p);

    if (p != -1) {          // If not empty input
        len = 1;
        maxlen = 1;

        while (scanf("%d", &c) == 1 && c != -1) {
            if (p < c) {                    // Extending streak
                len++;
            } else {                        // Streak broken
                if (len > maxlen)           // Save if better
                    maxlen = len;
                len = 1;                    // Reset
            }
            p = c;                          // Slide window
        }
        // POST-LOOP: check the LAST active streak
        if (len > maxlen) maxlen = len;
    }
    printf("%d\n", maxlen);
    return 0;
}
```

**Dry Run — Input: `3 2 1 3 5 -1`**
| Step | p | c | p<c? | len | maxlen | Action |
|------|---|---|------|-----|--------|--------|
| Init | 3 | — | — | 1 | 1 | First number |
| Read 2 | 3 | 2 | ❌ | 1 | 1 | maxlen stays 1, len→1, p=2 |
| Read 1 | 2 | 1 | ❌ | 1 | 1 | maxlen stays 1, len→1, p=1 |
| Read 3 | 1 | 3 | ✅ | 2 | 1 | len→2, p=3 |
| Read 5 | 3 | 5 | ✅ | 3 | 1 | len→3, p=5 |
| Read -1 | — | — | — | 3 | 1 | Loop exits |
| Post-loop | — | — | — | 3 | **3** | 3 > 1 → maxlen=3 |

**Output: `3`** (the subsequence is `1 3 5`) ✓

**What would NPTEL ask about this?**

❓ What is the output for input `9 2 4 0 3 4 6 9 2 -1`?
✅ `5` — the longest streak is `0 3 4 6 9` (length 5).
💡 Trace each step: 9→break(len=1), 2→ext(2 4, len=2), 0→break(max=2, len=1), 3→ext(0 3,len=2), 4→ext(len=3), 6→ext(len=4), 9→ext(len=5), 2→break(max=5, len=1). Post-loop: 1<5, maxlen stays 5.

❓ Why is `len = 1` (not 0) when a streak resets?
✅ The current number `c` itself starts a new streak of length 1.
💡 The reset number is NOT discarded — it becomes the first element of the new potential streak.

❓ Why is there a post-loop `if (len > maxlen) maxlen = len;`?
✅ If the longest streak is the **last one in the input**, no "break" occurs to trigger the `maxlen` update inside the loop — only the sentinel `-1` exits the loop.
💡 Without this, input `1 2 3 -1` would output 1 instead of 3.

❓ What happens for input `5 -1` (single element)?
✅ `maxlen = 1` — one element always forms a streak of length 1.
💡 `p = 5, len = 1, maxlen = 1`. Loop reads -1 immediately, exits. Post-loop: 1 = 1, no update. Output: 1 ✓.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| No post-loop `maxlen` check | Misses longest streak if it ends the input | Always add `if (len > maxlen) maxlen = len;` after loop |
| `p >= c` instead of `p < c` for extend | Extends when equal (wrong — need **strict** increase) | Use `p < c` for strict increase |
| `len = 0` on reset instead of `len = 1` | Current number not counted | Reset to `len = 1` |
| Not initializing `maxlen = 0` | Wrong comparison | `int maxlen = 0;` |
| Updating `maxlen` only in extend branch | Never records streak lengths | Update `maxlen` in the **break** (else) branch |

### Quick Recall
- 4 variables: `p` (prev), `c` (curr), `len` (current streak), `maxlen` (best)
- `p < c` → extend: `len++`
- `p >= c` → break: update maxlen if `len > maxlen`, reset `len = 1`
- Slide window: `p = c` after every decision
- **Post-loop check is mandatory** — handles last streak

---

## 23. GCD with `while` Loop — Full Implementation & Loop Invariant

📅 **Week 2**

### Concept Summary
The `while` loop implementation of GCD uses a **temporary variable** inside the loop to avoid overwriting values needed for the modulo operation. The loop invariant `GCD(A,B) = GCD(a,b)` provides formal proof of correctness. A **precondition** (a ≥ b via swap) is established before the loop begins.

### Key Syntax / Rules Box
```c
// Inside the GCD while loop — MUST use temp variable:
while (b != 0) {
    t = a;       // Save a (needed for a % b)
    a = b;       // New a = old b
    b = t % b;   // New b = old a % old b   ← Uses t, not updated a!
}
// When loop exits: b = 0, a = GCD
```
- Wrong (WITHOUT temp): `a = b; b = a % b;` → uses new `a` for `%`, not original
- Temp `t` preserves `a`'s value before overwriting
- Swap precondition: `if (a < b) { t=a; a=b; b=t; }` before the loop

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int a, b, t;

    scanf("%d %d", &a, &b);

    // Step 1: Ensure a >= b
    if (a < b) {
        t = a; a = b; b = t;   // Cyclic exchange (3-step swap)
    }

    // Step 2: Euclidean loop
    // Invariant: GCD(original_a, original_b) = GCD(a, b) throughout
    while (b != 0) {
        t = a;           // Backup a (crucial!)
        a = b;           // a ← old b
        b = t % b;       // b ← old a % old b (using backup t)
    }

    // Loop terminated: b = 0
    // Invariant + GCD(a,0) = a → a is the GCD
    printf("GCD = %d\n", a);
    return 0;
}
```

**Dry Run — GCD(16, 9):**
| Iteration | a | b | t | t%b (new b) |
|-----------|---|---|---|-------------|
| Start | 16 | 9 | — | — |
| 1 | 9 | 7 | 16 | 16%9=7 |
| 2 | 7 | 2 | 9 | 9%7=2 |
| 3 | 2 | 1 | 7 | 7%2=1 |
| 4 | 1 | 0 | 2 | 2%1=0 |
| Exit | **1** | 0 | — | — |

**GCD(16,9) = 1** ✓

**What would NPTEL ask about this?**

❓ Why is `t = a; a = b; b = t % b;` needed instead of just `a = b; b = a % b;`?
✅ After `a = b`, `a` now holds old b's value. `a % b` would then compute `old_b % old_b = 0` always — wrong!
💡 `t` saves the original `a` so `t % b = original_a % original_b` — the correct Euclidean step.

❓ What is the loop invariant for GCD?
✅ `GCD(A, B) = GCD(a, b)` — the GCD of original inputs equals GCD of current a,b at all times.
💡 At termination: b=0, so GCD(a,0)=a → a is the answer.

❓ What is the output for GCD(8,6)?
✅ `2` — trace: (8,6)→(6,2)→(2,0). Loop exits: a=2. ✓
💡 Step 1: t=8, a=6, b=8%6=2. Step 2: t=6, a=2, b=6%2=0. Done.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `a=b; b=a%b;` without temp | `b` always becomes 0 (old_b % old_b) | Use temp: `t=a; a=b; b=t%b;` |
| Stopping when `a==0` | Wrong — should stop when `b==0` | `while (b != 0)` |
| Returning `b` instead of `a` | `b` = 0 at termination; `a` = GCD | `printf("%d", a)` after loop |
| Not swapping when `a < b` | Algorithm works (self-corrects in one step) but less clean | Swap with temp for clarity |

### Quick Recall
- GCD(a,b) = GCD(b, a%b) until b=0; answer is a
- Loop body: `t=a; a=b; b=t%b;` — temp is **essential**
- Swap if `a < b`: `t=a; a=b; b=t;`
- Invariant: `GCD(A,B) = GCD(a,b)` always holds
- GCD(x,0) = x by definition

---

## 24. Matrix Row-Sum-Squared Problem (Nested While Loops)

📅 **Week 2**

### Concept Summary
Given an m×n matrix, compute **Σ(rowsum²)** — sum each row, square the row sum, then sum all those squares. Uses **nested while loops**: outer iterates rows, inner iterates columns within each row. Key discipline: `rowsum` must be **reset to 0** for every new row inside the outer loop.

### Key Syntax / Rules Box
```c
// Formula: total = Σᵢ (Σⱼ A[i][j])²
// Outer loop: rows (0 to m-1)
// Inner loop: columns (0 to n-1)

squaresum = 0;       // Init ONCE before outer loop
rowindex = 0;
while (rowindex < m) {
    rowsum = 0;      // RESET for each new row (inside outer loop)
    colindex = 0;
    while (colindex < n) {
        scanf("%d", &a);
        rowsum += a;
        colindex++;
    }
    squaresum += rowsum * rowsum;   // Add squared row sum
    rowindex++;
}
```

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int m, n, a, rowindex, colindex;
    int rowsum, squaresum = 0;

    scanf("%d %d", &m, &n);   // Read matrix dimensions

    rowindex = 0;
    while (rowindex < m) {          // Outer: each row
        rowsum = 0;                 // CRITICAL: reset per row
        colindex = 0;
        while (colindex < n) {      // Inner: each column
            scanf("%d", &a);
            rowsum = rowsum + a;
            colindex++;
        }
        squaresum = squaresum + rowsum * rowsum;
        rowindex++;
    }
    printf("%d\n", squaresum);
    return 0;
}
```

**Example — 3×4 matrix:**
```
4  7  11  2    → rowsum = 24 → 24² = 576
1  1   2  4    → rowsum = 8  →  8² = 64
2  9   0 -1    → rowsum = 10 → 10² = 100
Total = 576 + 64 + 100 = 740
```

**What would NPTEL ask about this?**

❓ What happens if `rowsum = 0` is placed before the outer loop instead of inside it?
✅ Row 1's sum gets added to Row 0's sum — every `rowsum` accumulates all previous rows.
💡 `rowsum` must reset to 0 at the **start of each outer iteration**.

❓ How many total `scanf` calls execute for a 3×4 matrix?
✅ 12 (3 rows × 4 columns = m × n total calls).
💡 Every element must be read in order, row by row.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `rowsum = 0` before outer loop | Carries previous rows' values | Inside outer loop |
| `squaresum += rowsum` (not squared) | Sums row sums, not squares | `squaresum += rowsum * rowsum` |
| `colindex` not reset per row | Inner loop may not execute for row 2+ | `colindex = 0` inside outer loop |

### Quick Recall
- `squaresum = 0` → init once before outer loop
- `rowsum = 0` → reset inside outer loop (per row)
- `colindex = 0` → reset inside outer loop (per row)
- Total scanf calls = m × n
- Formula: outer accumulates `rowsum²`, inner accumulates `rowsum`

---

## 🗂️ Week 1 Topic Map (Complete)

```
Week 1 Topics (from transcript):
├── Topic 1: Introduction — Programming process, algorithms, flowcharts
├── Topic 2: GCD Algorithm — Naive vs Euclidean, modulo, variables
├── Topic 3: The Programming Cycle — Edit-compile-run, gcc, a.out
├── Topic 4: Tracing a Simple Program — printf, \n, comments, program counter
├── Topic 5: Variables — int, float, declaration, assignment, format specifiers
└── Topic 6: Operators — %, &&, ||, !, leap year, short-circuit evaluation
```

---

## 🗂️ Week 2 Topic Map (Complete)

```
Week 2 Topics (from transcript):
├── Topic 1: While Loop I — Structure, priming read, sentinel, flowchart
│           While Loop Example — Sum with sentinel, loop invariant
│           While Loop GCD — temp variable swap, invariant proof
├── Topic 2: Longest Increasing Subsequence I — Problem, sliding window
│           Longest Increasing Subsequence II — Implementation, boundary cases
│           Longest Increasing Subsequence III — Edge case (last streak), tracing
├── Topic 3: Do-While Loop — Structure, guaranteed execution, sentinel printing
├── Topic 4: Matrix Problem — Nested while loops, row-sum-squared
├── Topic 5: For Loops — Structure, equivalence to while, comma operator, sum of reciprocals
├── Topic 6: Matrix Trace — Nested for loops, diagonal condition i==j
├── Topic 7: Break Statement — Infinite loops, break with sentinel, flag alternative, break+for update
└── Topic 8: Continue Statement — Skip iteration, scanf return value, Pythagorean triples
```

---

## ⚡ Updated Ultimate Quick Recall Sheet (Exam Day — Complete)

**Operators**
- `=` assigns; `==` tests equality — the #1 C bug
- `%` = remainder; `a % b == 0` → b divides a
- `&&` = AND (both); `||` = OR (either); `!` = NOT (flips)
- `&&` short-circuits left→right; stops at first false
- `||` short-circuits left→right; stops at first true

**Loops**
- `while`: test first → 0 or more times
- `do-while`: body first → 1 or more times; needs `;` after `while(cond)`
- `for (init; test; update)`: init once, test before each, update after each
- `break` in `for` → update does **NOT** run
- `continue` in `for` → update **DOES** run; then test
- `break` exits the **loop**, NOT the `if`
- `while (1)` = infinite loop → needs `break` or `return`

**Input / Output**
- `scanf` needs `&` before every variable (except arrays)
- `scanf` returns count of items read → `== 1` to check success
- Space before `%c` in format string skips whitespace
- `getchar()` reads **everything** including `'\n'`
- `'x'` = char literal (single); `"x"` = string (double)
- `printf` stays on same line unless `\n` is included
- `\n` = newline (one character, backslash-n NOT forward slash)

**Memory & Types**
- Uninitialized variables = **garbage value** (undefined behaviour)
- Always init accumulators: `sum = 0`, `max = 0`, `len = 0`
- `int` = whole numbers; `float` = decimal (limited precision)
- `%d` → int; `%f` → float; `%c` → char; `%lf` → double (scanf)
- Variable names: case-sensitive, no starting digit

**Key Patterns**
- Swap: `t=a; a=b; b=t;` (3 steps, temp required)
- GCD loop: `t=a; a=b; b=t%b;` until `b==0`; answer is `a`
- GCD invariant: `GCD(A,B) = GCD(a,b)` throughout
- Trace diagonal: `if (i == j)` (0-indexed, both loops 0 to n-1)
- Streak tracking: extend if `p < c`; save+reset if `p >= c`; **post-loop check**
- Alternating sum: `if (i%2==0) sum-=i; else sum+=i;`
- Upper triangular: check `matrix[i][j] != 0` for `i>j` (outer `i=1..n-1`, inner `j=0..i-1`)
- Blank line detection: two consecutive `'\n'` — pre-init `current = '\n'`
- Priming read: read first value before `while`, re-read at **end** of loop body
- `rowsum = 0` inside outer loop — reset per row, never outside

**Flowchart Symbols**
- Oval = Start/End
- Parallelogram = Input/Output
- Rectangle = Process/Operation
- Diamond = Decision (yes/no)

**Compilation**
- `gcc file.c` → compiles → produces `a.out`
- `./a.out` → runs (`./ `required on Linux)
- Compile error → no executable produced
- `#include <stdio.h>` → required for `printf` and `scanf`

---

# 🧪 Graded Assignments — Week 1 & Week 2

---

## 🧪 Assignment 1 — Week 1

📅 **Week 1** | NPTEL Graded Assignment

---

### 📌 What This Assignment Tests at a Glance

```
Q1 → Variables + scanf + Arithmetic (* operator)
Q2 → if-else + Formula with integers + Case-sensitive output
Q3 → char type + %c in scanf + if-else if-else chain
```

---

### Q1 — Volume of a Cuboid

**What to do:** Read 3 integers (length, breadth, height). Multiply them. Print the result.

```
Formula:  Volume = Length × Breadth × Height
Input:    3 integers on one line
Output:   1 integer (the volume)
```

#### ✅ Solution
```c
#include <stdio.h>

int main() {
    int length, breadth, height, volume;

    scanf("%d %d %d", &length, &breadth, &height);  // Read all 3 at once

    volume = length * breadth * height;              // * is multiply in C

    printf("%d", volume);                            // No \n unless asked

    return 0;
}
```

#### 🔍 Line-by-Line (Plain English)
| Line | What it does |
|------|-------------|
| `int length, breadth, height, volume;` | Creates 4 integer boxes in memory |
| `scanf("%d %d %d", ...)` | Reads 3 numbers from input; `&` sends the address so scanf can store the value |
| `volume = length * breadth * height` | Calculates volume; `*` is multiply (not `×`) |
| `printf("%d", volume)` | Prints the integer; `%d` = format for int |

#### 🧪 Dry Runs
| Input | Calculation | Output |
|-------|------------|--------|
| `2 3 4` | 2×3×4 = 24 | `24` |
| `5 5 5` | 5×5×5 = 125 | `125` |
| `1 1 1` | 1×1×1 = 1 | `1` |

#### ❓ NPTEL MCQ Traps

❓ What happens if `&` is missing: `scanf("%d", length)` instead of `scanf("%d", &length)`?
✅ Undefined behaviour / crash — scanf needs the **address** of the variable, not the value.
💡 `&length` = "address of length box". Without `&`, scanf writes to a random memory location.

❓ Output for `2 3 4`?
✅ `24` — straightforward. The only trap is forgetting `&` in scanf.
💡 `2 × 3 × 4 = 24`. No overflow risk for small numbers.

❓ What if `printf("%d\n", volume)` is used instead of `printf("%d", volume)`?
✅ Prints `24` then a newline. NPTEL checks exact output — if spec says no newline, omit `\n`.
💡 Always match the output format exactly to the problem statement.

❓ What if `1000 1000 1000` is the input?
✅ `1000000000` — just barely fits in `int` (max ~2.1 billion). But `2000 2000 2000 = 8,000,000,000` overflows!
💡 For safety with large inputs, use `long int` and `%ld`.

#### ⚠️ Common Mistakes
| Mistake | What goes wrong | Fix |
|---------|----------------|-----|
| `scanf("%d", length)` — missing `&` | Crash / garbage | Always `&length` |
| `volume = length + breadth + height` | Adds instead of multiplies | Use `*` |
| `printf("%f", volume)` | Wrong format for int | Use `%d` |
| `int` overflow for large values | Garbage output | Use `long int` + `%ld` |

#### ⚡ Quick Recall
- Formula: `l * b * h` (three `*`)
- `scanf` always needs `&` before variable name
- `%d` prints integers; `%ld` for `long int`
- `*` = multiply in C (never `×`)

---

### Q2 — Voter Eligibility

**What to do:** Given a person's current age and an election year, check if they'll be ≥ 18 in that election year. Current year = 2026.

```
Formula:  Age in election year = current_age + (election_year - 2026)
Rule:     If age_in_election_year >= 18 → "Eligible", else → "Not Eligible"
Input:    2 integers: current_age  election_year
Output:   Eligible   OR   Not Eligible   (exact spelling, case-sensitive)
```

#### ✅ Solution
```c
#include <stdio.h>

int main() {
    int age, year;

    scanf("%d %d", &age, &year);

    if (age + (year - 2026) >= 18)
        printf("Eligible");
    else
        printf("Not Eligible");

    return 0;
}
```

#### 🔍 How the Formula Works (Plain English)

```
"How old will this person be at the election?"
= their current age + how many years until the election
= age + (election_year - 2026)

If election_year = 2028:  gap = 2028 - 2026 = +2 years in the future
If election_year = 2024:  gap = 2024 - 2026 = -2 years (past) — still valid C math
If election_year = 2026:  gap = 0 — no change
```

#### 🧪 Dry Runs
| Current Age | Election Year | Age at Election | ≥ 18? | Output |
|-------------|--------------|-----------------|-------|--------|
| 16 | 2028 | 16 + 2 = **18** | ✅ | `Eligible` |
| 15 | 2028 | 15 + 2 = 17 | ❌ | `Not Eligible` |
| 18 | 2026 | 18 + 0 = **18** | ✅ | `Eligible` |
| 17 | 2026 | 17 + 0 = 17 | ❌ | `Not Eligible` |
| 20 | 2024 | 20 + (−2) = **18** | ✅ | `Eligible` |

#### ❓ NPTEL MCQ Traps

❓ Output for age=16, year=2028?
✅ `Eligible` — 16 + 2 = 18, and 18 **≥** 18 is true.
💡 The condition is `>= 18` (greater than OR EQUAL). If it were `> 18`, exactly-18 would fail.

❓ What if `>=` is replaced with `>`?
✅ A person who will be exactly 18 incorrectly gets `Not Eligible`.
💡 Always use `>=` for "18 or older". `>` means "strictly more than 18".

❓ What if output is `printf("eligible")` (lowercase e)?
✅ Wrong — C output is case-sensitive. Must be exactly `Eligible`.
💡 `Eligible` ≠ `eligible` ≠ `ELIGIBLE`.

❓ Can `year - 2026` be negative?
✅ Yes — for past election years. C handles negative integers correctly. 20 + (−2) = 18.
💡 No special handling needed — normal integer subtraction works fine.

#### ⚠️ Common Mistakes
| Mistake | What goes wrong | Fix |
|---------|----------------|-----|
| `> 18` instead of `>= 18` | Rejects exactly-18-year-olds | Use `>=` |
| `age - (year - 2026)` | Subtracts instead of adds | `age + (year - 2026)` |
| `printf("eligible")` | Wrong case | `printf("Eligible")` |
| `printf("Not eligible")` | Wrong case | `printf("Not Eligible")` |

#### ⚡ Quick Recall
- Formula: `age + (year - 2026) >= 18`
- Use `>=` not `>` (18-year-olds ARE eligible)
- Output: `Eligible` / `Not Eligible` — exact case
- Negative gap (past year) is valid C arithmetic

---

### Q3 — Simple Calculator (+, −, *)

**What to do:** Read two integers and an operator symbol. Do the operation. Print result.

```
Input:    integer  operator  integer    (e.g.  5 + 3)
Operator: only +, -, or *  (guaranteed)
Output:   the result as an integer
```

#### ✅ Solution
```c
#include <stdio.h>

int main() {
    int a, b, result;
    char op;                             // operator is a CHARACTER, not int

    scanf("%d %c %d", &a, &op, &b);    // space before %c skips the space in input

    if (op == '+')                       // single quotes for char comparison
        result = a + b;
    else if (op == '-')
        result = a - b;
    else                                 // only +,-,* guaranteed → else = *
        result = a * b;

    printf("%d", result);

    return 0;
}
```

#### 🔍 Why `char` and Not `int`?

```
Input: 5 + 3
         ↑
    This is the CHARACTER '+', not a number.
    In C: char stores one character.
          int stores a number.
    Use char op;  and  scanf("%c", &op);
```

#### 🔍 The `%d %c %d` Format String

```
scanf("%d %c %d", &a, &op, &b)
       ↑   ↑   ↑
       |   |   reads integer into b
       |   reads ONE character into op (the space before %c skips whitespace)
       reads integer into a

Input "5 + 3":
  a = 5
  op = '+'   (the space before %c in format string eats the space in input)
  b = 3
```

> ⚠️ Without the space before `%c`, `op` would read the **space** between `5` and `+`, not the `+` itself!

#### 🧪 Dry Runs
| Input | a | op | b | Operation | Output |
|-------|---|----|---|-----------|--------|
| `5 + 3` | 5 | `+` | 3 | 5+3 | `8` |
| `10 - 4` | 10 | `-` | 4 | 10-4 | `6` |
| `6 * 7` | 6 | `*` | 7 | 6×7 | `42` |
| `3 - 9` | 3 | `-` | 9 | 3-9 | `-6` |

#### ❓ NPTEL MCQ Traps

❓ What is wrong with `if (op == "+")`?
✅ `"+"` is a **string** (double quotes), not a character. Char comparisons need **single quotes**: `op == '+'`.
💡 `'+'` = char (one symbol). `"+"` = string (array of chars). Different types — comparing them is a type error.

❓ Why must there be a space before `%c` in `"%d %c %d"`?
✅ Without it, `op` reads the **space character** `' '` that appears between `5` and `+` in the input.
💡 The space in the format string tells scanf to skip any whitespace before reading the character.

❓ What if input is `5 / 3` (division)?
✅ Falls into the `else` branch → computes `5 * 3 = 15` — **wrong**. But the problem guarantees only `+`, `-`, `*`, so this case won't appear.
💡 The `else` is safe **only** because the problem specification guarantees only three operators.

❓ What is the output for `3 - 9`?
✅ `-6` — `%d` prints negative integers correctly with the minus sign.
💡 `int` holds negative values; `printf("%d", -6)` prints `-6` automatically.

#### ⚠️ Common Mistakes
| Mistake | What goes wrong | Fix |
|---------|----------------|-----|
| `op == "+"` (double quotes) | Type mismatch | `op == '+'` (single quotes) |
| `int op` instead of `char op` | Can't store `+`, `-`, `*` properly | Use `char op` |
| `scanf("%d%c%d", ...)` — no space before `%c` | `op` captures the space, not the operator | Add space: `"%d %c %d"` |
| Three separate `if` blocks (not `else if`) | All three conditions evaluated independently | Use `else if` chain |
| `printf("%c", result)` | Prints ASCII symbol, not the number | Use `printf("%d", result)` |

#### ⚡ Quick Recall
- Operator is `char` → `char op;` + `%c` in scanf + single quotes in comparison
- Format: `"%d %c %d"` — the space before `%c` is critical
- `if-else if-else` chain — only one branch runs
- `else` without explicit `op == '*'` is safe only when inputs are guaranteed

---

### 🗂️ Assignment 1 — Summary Table

| Q | Topic tested | Key concept | Most common mistake |
|---|-------------|-------------|-------------------|
| Q1 | scanf + arithmetic | `*` multiplies; `&` in scanf | Missing `&` / using `+` instead of `*` |
| Q2 | if-else + formula | `>= 18`; case-sensitive output | Using `>` instead of `>=` |
| Q3 | char + %c + chain | single quotes; space before `%c` | `"+"` (double quotes) instead of `'+'` |

---

## 🧪 Assignment 2 — Week 2

📅 **Week 2** | NPTEL Graded Assignment

---

### 📌 What This Assignment Tests at a Glance

```
Q1 → for loop + modulo (even/odd check) + accumulator
Q2 → for loop + two-variable streak tracking (current/longest)
Q3 → 2D array (VLA) + nested for loops + below-diagonal indexing + early exit
```

---

### Q1 — Alternating Sum of First N Natural Numbers

**What to do:** Read N. Compute `1 − 2 + 3 − 4 + 5 − ... ± N`.
Rule: **odd numbers add, even numbers subtract**.

```
Input:   single integer N
Output:  single integer (the alternating sum)

Example: N=5 → 1−2+3−4+5 = 3
Example: N=4 → 1−2+3−4 = −2
```

#### ✅ Solution
```c
#include <stdio.h>

int main() {
    int n, i, sum = 0;    // sum MUST start at 0

    scanf("%d", &n);

    for (i = 1; i <= n; i++) {      // i goes 1, 2, 3, ..., N
        if (i % 2 == 0)             // even number → subtract
            sum = sum - i;
        else                        // odd number → add
            sum = sum + i;
    }

    printf("%d", sum);
    return 0;
}
```

#### 🔍 How It Works (Plain English)

```
Start with sum = 0.
Go through each number 1 to N one by one:
  - Is the number even? (i % 2 == 0)  →  subtract it
  - Is the number odd?  (else)         →  add it
Print the final sum.
```

#### 🧪 Dry Run — N = 5
| i | Even or Odd? | Action | sum after |
|---|-------------|--------|-----------|
| 1 | Odd | sum = 0 + 1 | **1** |
| 2 | Even | sum = 1 − 2 | **−1** |
| 3 | Odd | sum = −1 + 3 | **2** |
| 4 | Even | sum = 2 − 4 | **−2** |
| 5 | Odd | sum = −2 + 5 | **3** |

**Output: `3`** ✓

> 💡 **Quick pattern check:** Even N → answer = `−N/2`. Odd N → answer = `(N+1)/2`. Use this to verify dry runs, not for coding.

#### ❓ NPTEL MCQ Traps

❓ Output for N=1?
✅ `1` — loop runs once: i=1 is odd → sum = 0+1 = 1.
💡 `i <= n` includes 1 when n=1.

❓ Output for N=4?
✅ `-2` — 1−2+3−4 = −2. Negative integers print fine with `%d`.
💡 No special handling for negative output — `printf("%d", -2)` prints `-2`.

❓ What if `sum` is not initialized to 0?
✅ Garbage starting value → wrong answer always.
💡 **Always initialize accumulators before the loop.**

❓ What if loop starts at `i = 0` instead of `i = 1`?
✅ i=0 is even → sum = 0 − 0 = 0 (harmless), but the pattern shifts: number 0 is counted as the "first" even. This gives wrong results for most inputs.
💡 Natural numbers start at 1. Always `i = 1`.

❓ What if `i < n` instead of `i <= n`?
✅ Misses N (the last number). For N=5: sums only 1−2+3−4 = −2 instead of 3.
💡 Use `i <= n` to include N itself.

#### ⚠️ Common Mistakes
| Mistake | What goes wrong | Fix |
|---------|----------------|-----|
| `int sum;` (no `= 0`) | Garbage starting value | `int sum = 0` |
| `i = 0` instead of `i = 1` | Wrong alternating pattern | Start at `i = 1` |
| `i < n` instead of `i <= n` | Misses the last number | Use `i <= n` |
| Adding when even, subtracting when odd | Reversed sign | `if (i%2==0)` subtract; `else` add |

#### ⚡ Quick Recall
- `sum = 0` before loop — mandatory
- Loop: `for (i = 1; i <= n; i++)` — starts at 1, includes N
- Even (`i % 2 == 0`) → subtract; Odd (`else`) → add
- Pattern: N even → `−N/2`; N odd → `(N+1)/2`

---

### Q2 — Longest Consecutive Sequence of Even Numbers

**What to do:** Read N integers. Find the length of the longest **unbroken run** of even numbers. Any odd number breaks the run and resets the count.

```
Input:   first line = N (count of numbers)
         second line = N space-separated integers
Output:  single integer (length of longest even streak)

Example: N=7, numbers: 2 4 3 6 8 10 5
         Streaks: [2,4]=2, [6,8,10]=3
         Output: 3
```

#### ✅ Solution
```c
#include <stdio.h>

int main() {
    int N, x;
    int current = 0, longest = 0;   // current = active streak; longest = best so far

    scanf("%d", &N);

    for (int i = 0; i < N; i++) {
        scanf("%d", &x);

        if (x % 2 == 0) {           // Even → extend streak
            current++;
            if (current > longest)  // New best?
                longest = current;
        } else {                    // Odd → reset streak
            current = 0;
        }
    }

    printf("%d", longest);
    return 0;
}
```

#### 🔍 Two Variables Explained

```
current = "how many evens have I seen IN A ROW right now?"
longest = "what's the best streak I've seen SO FAR?"

Every time I see an even:  current goes up. If current > longest, update longest.
Every time I see an odd:   current resets to 0. (The streak is broken.)
```

#### 🧪 Dry Run — Input: `7` → `2 4 3 6 8 10 5`
| x | Even? | current | longest |
|---|-------|---------|---------|
| 2 | ✅ | 1 | 1 |
| 4 | ✅ | 2 | 2 |
| 3 | ❌ | 0 | 2 |
| 6 | ✅ | 1 | 2 |
| 8 | ✅ | 2 | 2 |
| 10 | ✅ | 3 | **3** |
| 5 | ❌ | 0 | 3 |

**Output: `3`** ✓

#### ❓ NPTEL MCQ Traps

❓ Output if ALL numbers are odd?
✅ `0` — `current` never increases; `longest` stays at 0.
💡 Initial `longest = 0` handles this edge case automatically.

❓ Output if ALL numbers are even?
✅ N — streak never breaks; `current` grows to N.
💡 `longest` = N since `current` keeps getting updated.

❓ Why is `longest` updated **inside the even branch** (not after the loop)?
✅ If the longest streak ends before the last element (like our dry run: last element 5 is odd), the streak is already in `longest` from inside the loop.
💡 If you only update `longest` after the loop, you'd miss streaks that ended mid-input.

❓ What does `x % 2 == 0` return for a negative even like `x = -4`?
✅ `0` (true) — `-4 % 2 == 0` in C. Negative even numbers are correctly detected.
💡 The `%` operator works on negative numbers in C; even negatives give remainder 0.

#### ⚠️ Common Mistakes
| Mistake | What goes wrong | Fix |
|---------|----------------|-----|
| `longest` updated only in `else` (odd branch) | Misses streaks ending at last element | Update inside the `if (x%2==0)` branch |
| `current = 1` on reset instead of `current = 0` | Streak is never truly reset | Reset to `0` on odd |
| `x % 2 == 1` for odd check | Fails for negative odd numbers (`-3 % 2 == -1`) | Use `else` instead |
| `longest = current` without checking `>` | Overwrites `longest` with smaller value | Only update `if (current > longest)` |

#### ⚡ Quick Recall
- `current` = active streak; `longest` = best ever
- Even → `current++` then `if (current > longest) longest = current`
- Odd → `current = 0`
- Both start at 0; update `longest` **inside the even branch**

---

### Q3 — Upper Triangular Matrix Check

**What to do:** Read an N×N matrix. Check if it is **upper triangular** — meaning every number **below the main diagonal is 0**. Print `1` if yes, `0` if no.

```
Upper triangular — diagonal and above: anything
                 — below diagonal:      must all be 0

Example (YES — upper triangular):        Example (NO):
1 1 1 1                                  1 2 3
0 4 1 1                                  4 5 6   ← 4 is below diagonal
0 0 0 1                                  7 8 9   ← 7,8 are below diagonal
0 0 0 1

Output: 1                                Output: 0
```

#### 🔍 What "Below Diagonal" Means

```
For a 4×4 matrix (0-indexed rows and columns):

Position (row, col):    Below diagonal when row > col
(0,0)(0,1)(0,2)(0,3)   → row 0: nothing below diagonal
(1,0)(1,1)(1,2)(1,3)   → (1,0) is below diagonal [1 > 0]
(2,0)(2,1)(2,2)(2,3)   → (2,0) and (2,1) are below diagonal
(3,0)(3,1)(3,2)(3,3)   → (3,0), (3,1), (3,2) are below diagonal

Condition: matrix[i][j] must be 0 for all i > j
```

#### ✅ Solution
```c
#include <stdio.h>

int main() {
    int n;
    scanf("%d", &n);

    int matrix[n][n];           // Variable-length array (needs C99)

    // Step 1: Read ALL elements into the matrix
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            scanf("%d", &matrix[i][j]);

    // Step 2: Check only the below-diagonal elements
    for (int i = 1; i < n; i++) {       // Start at row 1 (row 0 has nothing below)
        for (int j = 0; j < i; j++) {   // Only check columns 0 to i-1 (left of diagonal)
            if (matrix[i][j] != 0) {
                printf("0");            // Found a non-zero below diagonal
                return 0;              // Exit immediately — no need to check further
            }
        }
    }

    printf("1");                        // All below-diagonal elements were 0
    return 0;
}
```

#### 🔍 Loop Logic Explained (Step by Step)

```
Outer loop: i = 1, 2, 3, ..., n-1   (rows — skip row 0, nothing below diagonal there)
Inner loop: j = 0, 1, ..., i-1      (columns left of the diagonal for this row)

For a 4×4 matrix:
  i=1: check j=0         → checks matrix[1][0]
  i=2: check j=0, j=1    → checks matrix[2][0] and matrix[2][1]
  i=3: check j=0,1,2     → checks matrix[3][0], matrix[3][1], matrix[3][2]

If ANY of these is non-zero → print 0 and stop (not upper triangular)
If ALL pass → print 1 (is upper triangular)
```

#### 🧪 Dry Run — The Example Matrix
```
1 1 1 1
0 4 1 1
0 0 0 1
0 0 0 1
```
| i | j | matrix[i][j] | == 0? |
|---|---|-------------|-------|
| 1 | 0 | 0 | ✅ |
| 2 | 0 | 0 | ✅ |
| 2 | 1 | 0 | ✅ |
| 3 | 0 | 0 | ✅ |
| 3 | 1 | 0 | ✅ |
| 3 | 2 | 0 | ✅ |

All zero → **Output: `1`** ✓

#### ❓ NPTEL MCQ Traps

❓ Why does the outer loop start at `i = 1` and not `i = 0`?
✅ Row 0 has no elements below the diagonal — there are no rows above row 0. Starting at 1 avoids an empty inner loop (which would run 0 times anyway, so it's also harmless to start at 0).
💡 Starting at `i=1` is cleaner and more intentional.

❓ Why is the inner loop `j < i` and not `j < n`?
✅ We only check below-diagonal elements where column < row. Elements where `j >= i` are on or above the diagonal — they're allowed to be anything.
💡 `j < i` → only checks `matrix[i][j]` where `row > col` (below diagonal).

❓ What does `return 0` inside the checking loop do?
✅ Exits the **entire program** immediately after printing `0` — no need to check remaining elements.
💡 More efficient than using a flag. Always print first, then return.

❓ Is `int matrix[n][n]` valid C?
✅ Yes — it's a **Variable Length Array (VLA)**, valid in C99 and later. GCC defaults to C99+.
💡 In old C89/ANSI C, you'd need `malloc`. For NPTEL, VLA is fine.

#### ⚠️ Common Mistakes
| Mistake | What goes wrong | Fix |
|---------|----------------|-----|
| `j <= i` instead of `j < i` | Checks diagonal too (diagonal can be non-zero) | Use `j < i` |
| Not reading all elements in Step 1 | Some `matrix[i][j]` values are garbage | Always read all n×n elements first |
| Printing `1` inside the loop | Prints multiple times if many zeros pass | Print `1` only after **both** loops complete |
| `return 0` without `printf("0")` first | Exits silently with no output | Always `printf` before `return` |

#### ⚡ Quick Recall
- Upper triangular: `matrix[i][j] == 0` for all `i > j`
- Read all elements first (Step 1), then check (Step 2)
- Outer: `i = 1` to `n-1`; Inner: `j = 0` to `i-1` (`j < i`)
- Early exit: `printf("0"); return 0;` on first violation
- Print `1` only after both loops finish with no violation

---

### 🗂️ Assignment 2 — Summary Table

| Q | Topic tested | Key concept | Most common mistake |
|---|-------------|-------------|-------------------|
| Q1 | `for` loop + modulo | `sum=0`; `i=1`; `i<=n`; even→subtract | Not initializing `sum`; wrong loop bounds |
| Q2 | Streak tracking | `current`/`longest`; reset on odd; update in even branch | Updating `longest` only after loop |
| Q3 | 2D array + nested loops | `j < i` (below diagonal); early exit | Checking `j <= i`; not reading all elements |

---

## 🗂️ Combined Assignment Quick Reference

### Format Specifiers Used in Assignments
| Type | `scanf` | `printf` |
|------|---------|----------|
| `int` | `%d` | `%d` |
| `char` | `%c` | `%c` |
| `long int` | `%ld` | `%ld` |

### Output Strings — Exact Spelling Required
| Question | Correct output | Wrong versions |
|---------|---------------|----------------|
| Q2 Asgn 1 — eligible | `Eligible` | `eligible`, `ELIGIBLE` ❌ |
| Q2 Asgn 1 — not eligible | `Not Eligible` | `not eligible`, `Not eligible` ❌ |
| Q3 Asgn 2 — upper triangular | `1` or `0` | `Yes`/`No`, `true`/`false` ❌ |

### The `&` Rule in `scanf`
```
scanf("%d", &age)    ← needs &   (scalar variables)
scanf("%d", array)   ← no &      (arrays — array name is already an address)
```
