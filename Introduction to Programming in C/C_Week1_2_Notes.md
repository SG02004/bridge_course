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
15. [🧪 Assignment 1 Analysis](#-assignment-1-analysis)

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

## 🗂️ Master Comparison Table: `break` vs `continue`

| Feature | `break` | `continue` |
|---------|---------|------------|
| Effect | Exits **innermost loop** entirely | Skips rest of **current iteration** |
| In `for` loop | Skips **update + test** | Runs **update**, then **test** |
| In `while` loop | Exits immediately | Goes to **test** |
| Exits `if` statement? | ❌ No | ❌ No |
| Necessary? | No — replaceable by flag variable | No — replaceable by nested `if` |
| Execution after statement | First statement after the loop | Next iteration (if test passes) |

---

## 🗂️ Loop Selection Guide

| Situation | Preferred Loop |
|-----------|---------------|
| Number of iterations known in advance (matrix, sum 1 to n) | `for` |
| Iterations depend on input/condition (GCD, sentinel) | `while` |
| Body must execute at least once | `do-while` |
| Multiple exit conditions needed | `for` with flag OR `while (1)` with `break` |

---

## ⚡ Ultimate Quick Recall Sheet (Exam Day)

- **`=` vs `==`**: assign vs compare — the #1 C bug
- **`break` in `for`**: update does NOT run
- **`continue` in `for`**: update DOES run
- **`break` + `if`**: `break` exits the **loop**, not the `if`
- **`scanf` return**: number of items read; 0 = failure, -1 = EOF
- **Swap**: always needs 3 steps + temp (`t = a; a = b; b = t;`)
- **GCD stops**: when `b == 0`; answer is `a`
- **Trace diagonal**: `i == j` (0-indexed)
- **Blank line**: two consecutive `'\n'` characters
- **`getchar`**: reads whitespace; `scanf("%d")` skips whitespace
- **Init accumulators**: `sum = 0`, `max = 0`, `trace = 0` — never leave them uninitialized
- **Nested loops**: reset inner accumulators **inside** outer loop
- **`1/i`**: integer division = 0 for i > 1; use `1.0/i`
- **Infinite loop**: `while (1)` — needs `break` or `return` to exit
- **Flag variable**: 0 = not triggered, 1 = triggered; put in loop condition
- **`char` vs `int`**: use `%c` and `char` for operators/characters; `%d` and `int` for numbers
- **`if-else if-else`**: covers all branches; last `else` = default case
- **Integer overflow**: `volume = l * b * h` — if dimensions are large, result may overflow `int`; use `long` to be safe

---

## 🧪 Assignment 1 Analysis

📅 **Week 1** | NPTEL Graded Assignment

---

### Question 1 — Volume of a Cuboid

> **Task:** Read length, breadth, height of a cuboid → print its volume.
> **Formula:** `Volume = Length × Breadth × Height`

#### ✅ Correct Solution (Cleaned)
```c
#include <stdio.h>

int main() {
    int length, breadth, height, volume;

    scanf("%d %d %d", &length, &breadth, &height);  // Read 3 integers

    volume = length * breadth * height;              // Multiply all three

    printf("%d", volume);   // Print WITHOUT newline (as required)

    return 0;
}
```

#### 🔍 Explanation — Line by Line
| Line | What it does | Why it matters |
|------|-------------|----------------|
| `int length, breadth, height, volume;` | Declares 4 integer variables | All 4 must be declared before use |
| `scanf("%d %d %d", &length, &breadth, &height)` | Reads 3 space-separated integers | The `&` is mandatory — passes address to scanf |
| `volume = length * breadth * height` | Multiplies all three | `*` is the multiplication operator in C |
| `printf("%d", volume)` | Prints integer, no newline | NPTEL often checks exact output format |

#### ❓ NPTEL MCQ Traps

❓ What happens if you write `printf("%d\n", volume)` instead of `printf("%d", volume)`?
✅ A newline is printed after the number. NPTEL may or may not penalise this — but match the spec exactly.
💡 When the problem says "Print the volume" with no mention of newline, use `printf("%d", volume)`.

❓ What is the output if inputs are `2 3 4`?
✅ `24` (2 × 3 × 4 = 24)
💡 Straightforward multiplication — no traps here except forgetting `&` in scanf.

❓ What if inputs are `100 200 300`?
✅ `6000000` — fits in `int` (max ~2.1 billion). But `1000 1000 1000` = 1,000,000,000 — still fits. `2000 2000 2000` = 8,000,000,000 — **overflows int!**
💡 For very large inputs, use `long int` and `%ld`.

#### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Missing `&` in scanf: `scanf("%d", length)` | Undefined behaviour / crash | Always use `&` with scanf |
| Using `+` instead of `*` | Prints sum, not volume | Use `*` for multiplication |
| `int` overflow for large inputs | Wrong (garbage) answer | Use `long int` for safety |
| `printf("%f", volume)` | Wrong format specifier for int | Use `%d` for `int` |

#### Quick Recall
- Volume formula: `l * b * h` (three `*` operators)
- scanf needs `&` before each variable
- `%d` for int, `%ld` for long int
- Check for overflow when inputs could be large

---

### Question 2 — Voter Eligibility

> **Task:** Given current age and election year, check if person will be ≥ 18 in that year.
> **Formula:** `age_in_election_year = current_age + (election_year - 2026)`
> **Rule:** Print `Eligible` if ≥ 18, else `Not Eligible`

#### ✅ Correct Solution (Cleaned)
```c
#include <stdio.h>

int main() {
    int age, year;

    scanf("%d %d", &age, &year);          // Read current age and election year

    // Calculate age in election year and check eligibility
    if (age + (year - 2026) >= 18)        // Key formula embedded in condition
        printf("Eligible");
    else
        printf("Not Eligible");

    return 0;
}
```

#### 🔍 Explanation — Line by Line
| Line | What it does | Why it matters |
|------|-------------|----------------|
| `scanf("%d %d", &age, &year)` | Reads two integers | Current age first, then election year |
| `age + (year - 2026)` | Projects age to election year | `year - 2026` = years from now |
| `>= 18` | Checks eligibility threshold | 18 or older = eligible |
| `printf("Eligible")` | Exact string — case sensitive | Do NOT print `eligible` (lowercase) |

#### 🔍 Dry Run Examples
| Current Age | Election Year | Age in Election Year | Output |
|-------------|--------------|----------------------|--------|
| 16 | 2028 | 16 + (2028−2026) = 18 | `Eligible` |
| 15 | 2028 | 15 + 2 = 17 | `Not Eligible` |
| 20 | 2024 | 20 + (2024−2026) = 18 | `Eligible` |
| 18 | 2026 | 18 + 0 = 18 | `Eligible` |
| 17 | 2026 | 17 + 0 = 17 | `Not Eligible` |

> ⚠️ Note: `election_year - 2026` can be **negative** if the year is before 2026 — the formula still works correctly in C with negative integers.

#### ❓ NPTEL MCQ Traps

❓ What is the output for age = 16, year = 2028?
✅ `Eligible` — 16 + (2028 - 2026) = 16 + 2 = 18 ≥ 18
💡 Exactly 18 satisfies `>= 18`. If the condition were `> 18`, this would print `Not Eligible`.

❓ What if year = 2024 (past year) and age = 20?
✅ `Eligible` — 20 + (2024 - 2026) = 20 + (−2) = 18 ≥ 18
💡 Subtraction with negative result is valid C arithmetic.

❓ What if `>=` is changed to `>`?
✅ A person who will be exactly 18 would get `Not Eligible` — **wrong answer**.
💡 The threshold is **18 or older** → must use `>=`, never just `>`.

❓ What is the output for age = 17, year = 2026?
✅ `Not Eligible` — 17 + 0 = 17 < 18
💡 Current year is 2026, so `year - 2026 = 0` — age doesn't change.

#### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `> 18` instead of `>= 18` | Age exactly 18 is wrongly rejected | Use `>=` |
| Wrong formula: `age - (year - 2026)` | Subtracts instead of adds | `age + (year - 2026)` |
| `printf("eligible")` (lowercase) | Wrong output — C is case-sensitive | `printf("Eligible")` |
| Reading year before age | Logic works but reads wrong values | Read age first, then year (match problem spec) |
| Hardcoding `2026`: `age + year - 2026` | Correct **only** if current year is 2026 | This is intentional per problem statement |

#### Quick Recall
- Formula: `age + (year - 2026) >= 18`
- Use `>=` not `>` for ≥ 18 check
- Output strings are **case-sensitive**: `Eligible` / `Not Eligible`
- `year - 2026` can be 0 or negative — C handles negative int arithmetic correctly

---

### Question 3 — Simple Calculator (+, -, *)

> **Task:** Read two integers and an operator (`+`, `-`, or `*`), print the result.

#### ✅ Correct Solution (Cleaned)
```c
#include <stdio.h>

int main() {
    int a, b, result;
    char op;

    scanf("%d %c %d", &a, &op, &b);   // Read: integer, char operator, integer

    if (op == '+')
        result = a + b;
    else if (op == '-')
        result = a - b;
    else                               // Only +, -, * guaranteed → safe to use else
        result = a * b;

    printf("%d", result);

    return 0;
}
```

#### 🔍 Explanation — Line by Line
| Line | What it does | Why it matters |
|------|-------------|----------------|
| `char op` | Declares op as a character variable | Operators are single characters, not integers |
| `scanf("%d %c %d", &a, &op, &b)` | Reads int, char, int with spaces | The space before `%c` skips whitespace automatically |
| `op == '+'` | Compares char using single quotes | `'+'` is a char literal; `"+"` would be a string — wrong type |
| Final `else` | Handles `*` without explicit check | Safe because problem guarantees only +, -, * |

#### 🔍 Dry Run Examples
| Input | a | op | b | Result | Output |
|-------|---|----|---|--------|--------|
| `5 + 3` | 5 | `+` | 3 | 5+3 | `8` |
| `10 - 4` | 10 | `-` | 4 | 10-4 | `6` |
| `6 * 7` | 6 | `*` | 7 | 6*7 | `42` |
| `3 - 9` | 3 | `-` | 9 | 3-9 | `-6` |

#### ❓ NPTEL MCQ Traps

❓ Why is `op` declared as `char` and not `int`?
✅ Because `+`, `-`, `*` are **characters** (single symbols), not integers. `char` stores one character.
💡 Using `int op` would not work with `scanf("%c", &op)` correctly.

❓ What is wrong with `if (op == "+")`?
✅ `"+"` is a **string literal** (type `char *`), not a character. Should be `op == '+'` (single quotes).
💡 Classic NPTEL trap: single quotes `' '` for `char`, double quotes `" "` for strings.

❓ What does `scanf("%d %c %d", &a, &op, &b)` do with input `5 + 3`?
✅ Reads `a=5`, skips space, reads `op='+'`, skips space, reads `b=3`.
💡 The space in `"%d %c %d"` before `%c` is critical — without it, `op` may capture the space character `' '` instead of `'+'`.

❓ What if the operator is `/` (division)? What does the program print?
✅ It falls into the `else` branch and computes `a * b` instead — **wrong answer**.
💡 The `else` is only safe because the problem guarantees only `+`, `-`, `*`. If division were possible, you'd need `else if (op == '*')` and an explicit `else` for error.

❓ What is the output for `3 - 9`?
✅ `-6` — negative integers print correctly with `%d`.
💡 `int` can hold negative values; `%d` prints the sign automatically.

#### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `op == "+"` (double quotes) | Type mismatch: comparing char to char* | `op == '+'` (single quotes) |
| `int op` instead of `char op` | Cannot store character correctly | Use `char op` |
| `scanf("%d%c%d")` (no space before `%c`) | `op` captures space `' '` between number and operator | Add space: `"%d %c %d"` |
| Three separate `if` instead of `if-else if-else` | All three conditions evaluated; last assignment wins | Use `else if` chain |
| `printf("%c", result)` | Prints ASCII character, not the number | Use `printf("%d", result)` |

#### Quick Recall
- Operator is a `char` → use `%c` in scanf, single quotes in comparison
- Always space before `%c` in scanf format string: `"%d %c %d"`
- `if-else if-else` chain — only one branch executes
- `else` as final catch is safe **only** when inputs are guaranteed
- `%d` prints integers (including negatives) correctly

---

## 🗂️ Assignment 1 — Concept Map

```
Assignment 1 Tests:
├── Q1: Variables + Arithmetic operators (*) + printf/scanf
├── Q2: Conditional (if-else) + Formula evaluation + Integer arithmetic
└── Q3: char type + %c format specifier + if-else if-else chain
```

| Concept | Tested in | Key thing to remember |
|---------|-----------|----------------------|
| `int` declaration & scanf | Q1, Q2, Q3 | `&` before variable name in scanf |
| Arithmetic `*` operator | Q1 | Not `×` — use `*` in C |
| `if-else` | Q2, Q3 | Use `>=` for "18 or older"; `else if` for chains |
| `char` type & `%c` | Q3 | Single quotes for char literals: `'+'` not `"+"` |
| scanf format spacing | Q3 | Space before `%c` to skip whitespace |
| Integer output `%d` | Q1, Q2, Q3 | Works for positive and negative integers |
