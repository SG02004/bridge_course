# 🎯 C Programming — Exam Notes (built from all 64 NPTEL "Introduction to Programming in C" lecture slides)

> **Purpose:** one file to revise from — MCQ, fill-in-the-blank, find-the-error, output-prediction and trace questions.
>
> **Source:** all 64 `mooc-*.pptx` decks in this folder (NPTEL "Introduction to Programming in C", IIT Kanpur).

---

## How to use this file (in the order below if you are short on time)

| Time left | Do this |
|---|---|
| **6+ hours** | Read 1 → 16 in order, then work through the question banks 17 → 20. |
| **3 hours** | Read 2 (types/IO), 4 (operators), 5–6 (control flow/loops), 7–7b (functions/pointers), 8–10b (arrays/strings/pointers), then the banks. |
| **1 hour** | Read **21 (cheat sheet)** + every ⚠️ box + the answer keys of 17–20. |
| **15 minutes** | Read **21c (last-minute facts)** and the 10-minute self-test at the end. |

---

## The 5 question types and exactly how to attack each

| Type | What the paper tests | Your method |
|---|---|---|
| **MCQ (concept)** | Definitions, keywords, headers, modes | Recall the tables in 2 (types/specifiers), 9 (strings), 14 (file modes) and 21 (cheat sheet). |
| **MCQ (output prediction)** | Precedence, `++`/`--`, integer division, `%`, loop count, `printf` format | Trace **one line at a time** in a table of variable values. Never guess. |
| **Fill in the blank** | Missing keyword / operator / header / library function | Identify the *category* first (keyword? header? function?), then fill. |
| **Find the error** | Missing `;`, wrong format specifier, `=` vs `==`, missing `&`, bad pointer, array bounds | Check in this order: `;` → `&` in scanf → `=` vs `==` → `%` specifier → bounds. |
| **Trace / dry-run** | Loop iterations, recursion stack, pointer moves | Table with one column per variable, one row per iteration. |

### ⏱️ Top 25 rules that decide most marks

1. C is **case-sensitive** (`Main` ≠ `main`).
2. Every **statement ends with `;`** — but `#include`, `#define`, `if(...)`, `while(...)`, `for(...)` do **not** take one.
3. Array index starts at **0**; last element of `a[n]` is `a[n-1]`.
4. `=` assigns, `==` compares.
5. `0` is **false**, any **non-zero** value is **true**.
6. `&&`, `||`, `!` are logical; `&`, `|`, `^`, `~` are bitwise.
7. `&&` and `||` **short-circuit** (right side may never run).
8. `i++` uses the **old** value then increments; `++i` increments **then** uses.
9. Integer / integer = **integer** (fraction is thrown away, it does **not** round).
10. `scanf` needs **addresses** (`&x`) — except arrays/strings (`scanf("%s", str)`).
11. C passes arguments **by value** — a function cannot change a caller's variable unless you pass a **pointer**.
12. Array name **decays** to a pointer to its first element; `a[i]` ≡ `*(a+i)`.
13. Strings end with `'\0'`; that `'\0'` is **not counted** by `strlen` and **not printed** by `%s`.
14. `break` leaves the **nearest** loop or `switch`; `continue` jumps to the next iteration.
15. `do { } while(expr);` — **always runs at least once** and needs a **semicolon** after `while(expr)`.
16. `sizeof` is an **operator**, not a function; it returns bytes (`size_t`, print with `%zu`).
17. `ptr + i` == `ptr + i * sizeof(type)` bytes.
18. Returning the address of a **local variable** gives a **dangling pointer** (undefined behaviour).
19. `fopen` returns a **`FILE *`**, or **`NULL`** on failure.
20. `"r"` requires an existing file; `"w"` truncates/creates; `"a"` appends.
21. The **order in which function arguments are evaluated is unspecified** in C.
22. Modifying the same variable twice between sequence points (`i = i++ + ++i;`) is **undefined behaviour**.
23. Out-of-bounds array access is **not** caught by the compiler — it is undefined behaviour.
24. `float` → `int` **truncates toward zero** and can be undefined if the value does not fit.
25. If the code has **undefined behaviour**, the correct exam answer is *"undefined / unpredictable"*, not the value your compiler happens to print.

### ⚠️ The single biggest scoring trap
NPTEL loves questions whose answer is **"undefined behaviour"** or **"the compiler decides"**. Learn these five:
`i = i++ + ++i;` · `a[i] = i++;` · `f(a=b+1, b=a+1);` · returning a pointer to a local · out-of-bounds indexing.

---

## Table of Contents

| # | Topic | Lecture decks |
|---|---|---|
| 1 | Program structure, compilation cycle, files & directories | mooc-03, 04 |
| 2 | Data types, variables, `char` & ASCII | mooc-05, 06, 20, 21 |
| 3 | Type conversion & casting | mooc-08 |
| 4 | Operators, expressions, precedence & associativity | mooc-26, 26-a, 27 |
| 4b | `%`, `++`/`--`, logical operators, side effects | mooc-11, 26-a, 27 |
| 5 | Conditionals: `if`, `if-else`, comparison operators, `switch` | mooc-09, 10, 68, 69 |
| 6 | Loops: `while`, `do-while`, `for`, `break`, `continue` | mooc-12, 12-a, 13, 14, 14-a, 14-b, 17, 18, 18-a, 19, 22, 23, 24, 25 |
| 7 | Functions — anatomy, calls, scope and the stack | mooc-28, 29, 31, 33 |
| 7b | Functions that change the caller; designing functions | mooc-31, 33, 44 |
| 8 | Arrays | mooc-36, 37, 38, 39, 40, 45, 46 |
| 9 | Strings & character arrays | mooc-40, 41, 48-a |
| 10 | Pointers — addresses, dereferencing, arithmetic, `sizeof` | mooc-42, 43, 44, 47 |
| 10b | Passing arrays/subarrays, the heap (`malloc`/`free`), dangling pointers | mooc-45, 46, 48, 48-a |
| 11 | Recursion | mooc-50, 51, 51-a |
| 12 | Structures | mooc-60 |
| 13 | Multi-dimensional arrays & C type expressions | mooc-54, 55, 56, 57 |
| 14 | File handling | mooc-61, 62, 68, 69 |
| 15 | Preprocessor, multiple source files & makefiles | mooc-64, 65 |
| 16 | Linked lists (singly) | mooc-62-1 |
| 16b | Doubly linked lists | mooc-62-2, 62, 64 |
| **17** | **Practice MCQs — Set 1 (Q1–Q30)** | revision |
| **17b** | **Practice MCQs — Set 2 (Q31–Q50)** | revision |
| **17c** | **Practice MCQs — Set 3 (Q51–Q80)** | revision |
| **18** | **Fill-in-the-blank bank 1–58** | revision |
| **18b** | **Fill-in-the-blank bank 59–98** | revision |
| **18c** | **Fill-in-the-blank bank 99–128** | revision |
| **19** | **Find-the-error bank (E1–E32)** | revision |
| **20** | **Output-prediction drill — Set 1 (O1–O30)** | revision |
| **20b** | **Output-prediction drill — Set 2 (O31–O62)** | revision |
| **21** | **Cheat sheet — all the tables** | revision |
| **21b** | **Equivalences & sizes to remember** | revision |
| **21c** | **Last-minute facts & self-test checklist** | revision |

---

## 1. Program structure, compilation cycle, files & directories

### Concept Summary
* A **file** is the unit of data in a system — a collection of bytes on secondary storage. A **directory** groups files; the one you work in is the **current working directory**.
* The **programming cycle**: *Write/Edit → Compile → Run → (if output wrong) edit again*.
* Compilation has **4 stages** — this is a favourite fill-in-the-blank.

| Stage | What runs | Input | Output |
|---|---|---|---|
| 1 | **C preprocessor** | `.c` + included `.h` | expanded source (comments removed, `#` directives handled) |
| 2 | **Compiler** | expanded source | assembly |
| 3 | **Assembler** | assembly | **object code `.o`** |
| 4 | **Linker** | `.o` files + libraries | **executable** (`a.out`) |

* `gcc` by default produces **`a.out`** in the current working directory.

### Key Syntax / Rules Box
```c
#include <stdio.h>        /* preprocessor directive — NO semicolon */
int main()                /* execution starts here */
{
    printf("Hello\n");    /* every statement ends with ; */
    return 0;             /* returning from main ends the program */
}
```

### Command-line box (fill-in-the-blank gold)
| Command | Meaning |
|---|---|
| `gcc prog.c` | compile — output is `a.out` |
| `gcc -o prog prog.c` | compile, name the executable `prog` |
| `gcc -c prog.c` | compile only → `prog.o` (object code; no `main` required) |
| `gcc -o a.out prog.o list.o` | **link** object files into an executable |
| `./a.out` | run the program in the current directory |
| `gcc file.c -lm` | link the **math** library (needed for `sqrt`) |

### Statement vs Block
* An **expression** becomes a **statement** when you put a **`;`** after it: `x = 0;`
* `{ ... }` groups declarations + statements into a **compound statement (block)**, which is *syntactically equivalent to a single statement*. That is why an `if`/`while` can control a whole block.

### End of file
* On the terminal, **end-of-file is `Ctrl-D`**, which is **EOT, ASCII value `\x4`**.
* `getchar()` returns **`EOF`** after end-of-file, so its result must be stored in an **`int`**, never a `char`.
* `feof(stdin)` returns **non-zero (1)** once EOF has been seen.

### EOF / line-counting program from the slides (memorise the shape)
```c
#include <stdio.h>
int read_next_line();                 /* forward declaration */
int read_all_lines() {
    int linecnt = 0, isvalid;
    while (!feof(stdin)) {            /* stop at end of file */
        isvalid = read_next_line();
        linecnt = linecnt + isvalid;
    }
    return linecnt;
}
int read_next_line() {
    int ch, flag = 0;
    ch = getchar();
    while (ch != EOF && ch != '\n') { flag = 1; ch = getchar(); }
    return flag || (ch == '\n');      /* 1 = a line was consumed (a blank line also counts) */
}
int main() { read_all_lines(); }
```

### ⚠️ Traps
* `#include <stdio.h>;` — **no semicolon**. Adding one is a classic "find the error".
* `main` must be **lower-case**; `Main()` is a different symbol and will not be found by the linker.
* `gcc -c` **does not** produce an executable — you need the linker.
* `feof(fp)` becomes true only **after** an attempt to read past the end; testing it *before* the read is the standard bug.
* A **file** and a **directory** are different: `a.out` is created **in** the directory you are in.

### Quick Recall
* Preprocessor → compiler → assembler → **linker** → `a.out`.
* `stdio.h` = I/O · `stdlib.h` = `malloc`/`calloc`/`free` · `string.h` = `strlen`/`strcpy`/`strcmp`/`strcat` · `math.h` = `sqrt` (**link with `-lm`**).

---

## 2. Data types, variables, `char` & ASCII

### Concept Summary
* A **variable** is "a name for a box". `int a, b, g;` = three integer boxes. Assignment **replaces** whatever was stored.
* Declaration = giving a type and a name; **definition/initialisation** = also giving a value (`int b = 4;`).
* C's basic types and **typical** sizes (machine dependent!):

| Type | Typical size | `printf` | `scanf` | Notes |
|---|---|---|---|---|
| `char` | 1 byte | `%c` | `%c` | also a small integer (ASCII code) |
| `int` | 4 bytes | `%d` | `%d` | |
| `unsigned int` | 4 bytes | `%u` | `%u` | never negative |
| `float` | 4 bytes | `%f` | `%f` | ~6–7 significant digits |
| `double` | 8 bytes | `%f` or `%lf` | `%lf` | use for heavy float maths |
| `long int` | 4 or 8 | `%ld` | `%ld` | `%lu` for unsigned |
| string | — | `%s` | `%s` | `char` array ending in `'\0'` |
| pointer | — | `%p` / `%lu` | — | |
| octal / hex | — | `%o` / `%x` | `%o` / `%x` | `%e` scientific · `%%` prints `%` |

* `printf` returns the **number of characters printed**; `scanf` returns the **number of items successfully read**.

### ASCII facts you must know cold
| Character | Code | Character | Code |
|---|---|---|---|
| `'\0'` (NULL) | 0 | `'A'` | 65 |
| `'0'` | 48 | `'a'` | 97 |

* Digits, upper-case letters and lower-case letters are each **consecutive** in ASCII, in alphabet order.
* ⇒ `ch - '0'` turns a digit character into its numeric value; `ch - 'a' + 'A'` turns lower case into upper case.

```c
/* print the alphabet — a classic output question */
char ch;
for (ch = 'A'; ch <= 'Z'; ch = ch + 1)
    printf("%c", ch);          /* ABCDEFGHIJKLMNOPQRSTUVWXYZ */
```

### Character-case tests (frequent fill-in-the-blank)
```c
if (ch >= 'A' && ch <= 'Z') printf("Upper case\n");
if (ch >= 'a' && ch <= 'z') printf("Lower case\n");
if (ch >= '0' && ch <= '9') printf("Digit\n");
if (ch >= 'a' && ch <= 'z') ch = ch - 'a' + 'A';   /* convert to upper case */
```

### `scanf` usage
```c
scanf("%d%d", &x, &y);      /* two integers */
scanf("%f", &a);            /* one float */
scanf("%s", str);           /* string — NO & because str is already an address */
scanf("%d", &num[i]);       /* array element — &num[i] means &(num[i]) */
```
* `%d`, `%f`, `%s` **skip leading whitespace**; they do **not** care whether the input is on one line or many.
* `%c` does **not** skip whitespace.

### ⚠️ Traps
* `scanf` needs **addresses** (`&x`) — except for arrays/strings. Missing `&` is the most common "find the error".
* `scanf("%d", &n); scanf("%c", &c);` → `c` reads the **leftover newline**. Fix: `scanf(" %c", &c)` (leading space).
* Reading `12` with `%d` stores the *integer* 12; reading `1` with `%c` stores the *character* `'1'` = ASCII **49**.
* `scanf("%f", &d)` on a `double` is a bug — use **`%lf`**. (`printf` is more forgiving.)
* Uninitialised local variables hold **garbage** — printing them gives *undefined* output.
* `char` and `int` widths: `'1'` occupies 1 byte, `12` occupies 4 bytes.
* Values never fit exactly: `float` cannot represent every integer exactly (`10000009` became `10000008.000000` after `(float)`).

### Quick Recall
* `sizeof(char)`=1, `sizeof(int)`=4, `sizeof(float)`=4, `sizeof(double)`=8 (typical).
* `char` behaves like an integer in arithmetic and comparisons because that is what it stores.
* Assignment vs initialisation: `int b = 4;` initialises; `b = 4;` assigns after definition.

---

## 3. Type conversion & casting

### Concept Summary
Two ways to convert a value from one type to another:
1. **Implicit (automatic)** — happens when types are mixed in an expression, or when a value is assigned/copied to a variable of a different type.
2. **Explicit (cast)** — `(int) x`, `(float) y`. A cast is an **expression**: it converts the value and can be used anywhere a value of that type can be used. It does **not** change the original variable.

### The four cases from the slides
| Conversion | Result | Verdict |
|---|---|---|
| `int` → `float` (small → large) | usually fine, but large ints **lose digits** | "may give unexpected results" |
| `float` → `int` (large → small), value fits | **truncates** the fraction: `5.674157` → `5` | loss of information |
| `float` → `int`, value does **not** fit (`1.0E50`) | garbage (`-2184748364`) | **undefined** |
| `char` ↔ `int` | ASCII code both ways | always safe |

```c
float x = 5.67;  int y;
y = x;                    /* implicit: y becomes 5 (truncated, NOT 6) */
printf("%d", (int) x);    /* explicit cast: prints 5 */
```
```c
int y = 10000009;
printf("%f", (float) y);  /* prints 10000008.000000  — precision LOST */
printf(" %d", y);         /* prints 10000009 */
```
```c
float x = 1.0E7;  y = (int) x;   /* 10000000  — fits, fine */
float x = 1.0E50; y = (int) x;   /* -2184748364 — too large, UNDEFINED */
```

### Promotion rules in mixed expressions
* If one operand is `float`/`double` and the other is `int`, the integer is **promoted** to floating point.
* ⇒ `1/2` is **0**, but `1/2.0` is **0.5**. `(float)1/2` is **0.5**; `1/(float)2` is **0.5**.
* `char` is promoted to `int` in arithmetic.

### ⚠️ Traps
* `float`→`int` **truncates toward zero**, it does **not** round. `(int)5.99` = `5`, `(int)-5.99` = `-5`.
* To round: `(int)(x + 0.5)`.
* Casting a **larger** type into a **smaller** one is where undefined behaviour appears.
* Assigning `float` to `int` via `=` (implicit) behaves exactly like the explicit cast — *"same answer is obtained for both programs"*.
* `a % b` with `float`/`double` operands is a **compile error** — `%` is integer-only.
* `psize = sizeof(x)` stored in an `int` is legal but `sizeof` returns `size_t` (unsigned); comparing `sizeof(x) > -1` is a classic bug because the `-1` is converted to a huge unsigned value.

### Quick Recall — integer arithmetic
| Expression | Value | Why |
|---|---|---|
| `7/2` | `3` | truncation |
| `-7/2` | `-3` | truncation toward zero |
| `7%2` | `1` | remainder |
| `-7%2` | `-1` | sign follows the **left** operand |
| `7.0/2` | `3.5` | one operand is floating point |
| `7/2.0` | `3.5` | one operand is floating point |
| `1 + 2.0` | `3.0` | `int` promoted to `double` |

---

## 4. Operators, expressions, precedence & associativity

### Concept Summary
* An **expression** is the basic unit of evaluation and **returns a value of a type**. The RHS of `=` is an expression; so is `(a*a)+(b*b)`, made of sub-expressions `a*a` and `b*b`.
* Expressions are built from **atoms** (constants/variables) combined by **operators** — unary (`-`, `!`) or binary (`+`, `*`).
* **Precedence** decides which operator binds first when the operators are *different*.
* **Associativity** decides the order when the *same* operator repeats.

### The precedence table — the single most tested table
| Class | Operators | Associativity |
|---|---|---|
| **(Highest)** Postfix | `()  []  .  ->  ++  --` | Left → right |
| Unary | `!  -  +  &  *  sizeof  (type)  ++  --` | **Right → left** |
| Multiplicative | `*  /  %` | Left → right |
| Additive | `+  -` | Left → right |
| Relational | `<  <=  >  >=` | Left → right |
| Equality | `==  !=` | Left → right |
| Logical AND | `&&` | Left → right |
| Logical OR | `\|\|` | Left → right |
| Conditional | `?:` | Right → left |
| Assignment | `=  +=  -=  *=  /=  %=` | **Right → left** |
| **(Lowest)** Comma | `,` | Left → right |

* The table is part of the **specification of the C language** (not of one compiler).
* Memory hook for the middle: **"Multiply before Add, Add before Compare, Compare before And, And before Or, and Assign last."**

### Assignment is right-associative
```c
a = b = c = d = e = 0;          /* means  a = (b = (c = (d = (e = 0)))) */
```
Why it works: `=` **assigns to the left operand** (which must be a **variable**) **and then returns the assigned value and type**. So `(e=0)` yields `0`, which is assigned to `d`, and so on. This is the standard mathematical convention of initialising several variables to the same value.

Evaluation of `a = (b = 10)`:
1. Evaluate the parenthesised expression `(b = 10)`: `b` becomes 10, the expression **returns 10**.
2. The whole expression reduces to `a = 10`; `a` becomes 10 and 10 is returned.

### Binary `+` and `-` are left-associative
```c
a + b + c + d        /* ((a+b)+c)+d */
a - b - c - d        /* ((a-b)-c)-d */
printf("%d", 10-5-15);   /* ((10-5)-15) = -10 */
```

### Worked evaluations from the slides
| Expression | Grouping | Value |
|---|---|---|
| `10 - 5 - 15` | `((10-5)-15)` | **-10** |
| `a = 10 + 5 * 4 % 2` | `a = (10 + ((5*4) % 2))` = `10 + (20%2)` = `10 + 0` | **10** |
| `a + b - c * d % e / f` | `(a+b) - (((c * d) % e) / f)` | depends on values |
| `a <= b && b >= c` | `(a<=b) && (b>=c)` | 0 or 1 |

### ⚠️ Traps
* `=` vs `==` — `if (x = 0)` is an **assignment**, always false. Not a comparison.
* `&` (address-of / bitwise AND) vs `&&` (logical AND) — different operators, different meaning.
* `sizeof` is an **operator**, so `sizeof x` and `sizeof(x)` are both legal, and `sizeof` binds tighter than arithmetic.
* The unary operators being **right-to-left** is why `- - a` works and why `*p++` means `*(p++)`.
* A **cast** `(int)x` is also unary — do not confuse `(int)x` with a function call.

### Quick Recall
* Precedence: `()` `[]` → unary → `* / %` → `+ -` → relational → equality → `&&` → `||` → `?:` → `=` → `,`.
* Associativity: everything left-to-right **except** unary, `?:` and `=` which are right-to-left.

---

## 4b. `%`, `++`/`--`, logical operators, side effects

### The `%` (remainder) operator
* For integers `a` and `b`, **`a % b` is the integer remainder** when `a` is divided by `b`. `8 % 3` is **2**.
* Uses from the slides: `if (a % 6 == 0)` tests divisibility by 6; `a % 2 == 0` tests even; `a % 10` gives the last digit; `a / 10` drops the last digit.
* **`%` cannot be applied to `float` or `double`** — that is a compile error.
* Negative operands: the result follows the sign of the **left** operand. `-7 % 2` = `-1`; `7 % -2` = `1`.

### `++` and `--`
```c
int a = 5, b;
b = a++;    /* POSTFIX: b gets the OLD value 5, then a becomes 6  */
b = ++a;    /* PREFIX : a becomes 6 first, then b gets the NEW value 6 */
```
* Both have **side effects** — they modify the variable.
* As an expression, `a++` yields the old value; `++a` yields the new value.
* `i++` alone as a statement (`i++;`) is identical to `++i;` — no difference when the value is not used.

### Logical vs bitwise operators
| Logical (0/1 result) | Bitwise (bit-by-bit) | Meaning |
|---|---|---|
| `&&` | `&` | AND |
| `\|\|` | `\|` | OR |
| `!` | `~` | NOT |
| — | `^` | XOR (exclusive OR) |

* **Short-circuit evaluation:** in `a && b`, if `a` is false (`0`) then `b` is **never evaluated**. In `a || b`, if `a` is true then `b` is **never evaluated**.
* `a && b` evaluates to **1 or 0**, never to the value of `b`.
* This is why `if (p != NULL && p->x > 0)` is safe but `if (p->x > 0 && p != NULL)` is not.

```c
/* truth table for && and || */
1 && 1 = 1    0 || 0 = 0
1 && 0 = 0    1 || 0 = 1
!0 = 1        !5 = 0
```

### Side effects, sequence points and undefined behaviour (top UB questions)
```c
i = i++ + ++i;               /* UNDEFINED BEHAVIOUR */
a[i] = i++;                  /* UNDEFINED BEHAVIOUR */
printf("%d %d", i++, i++);   /* ORDER OF EVALUATION UNSPECIFIED */
x = f(a=b+1, b=a+1);         /* arguments may be evaluated L→R or R→L */
return &local;               /* dangling pointer — UNDEFINED */
a[n] = 0;  /* n out of bounds — UNDEFINED */
```
> **Rule:** you may **read** a variable as many times as you like, but if you **modify it twice**, or **modify and read it**, without an intervening **sequence point**, the behaviour is **undefined**. Sequence points include `;`, the `&&`, `||`, `?:` and `,` operators, and the point at which a function is called.
>
> In an exam, if a code snippet is UB, the correct answer is *"undefined / compiler dependent / cannot be determined"* — even if you know what your compiler prints.

### The argument-evaluation-order example from the slides
```c
int f(int a, int b) { return b - a; }
main() { int a = 2, b = 1;  a = f( a=b+1, b=a+1 );  printf("%d %d", a, b); }
```
* **Rule:** all arguments are evaluated **before** the call is made, but C does **not specify the order**.
* Left-to-right assumed: `a=b+1` → `a=2, b=1`; then `b=a+1` → `b=3`. Call `f(2,3)` = `1` → output **`1 3`**.
* Right-to-left (what the compiler actually did on the slide's machine): `b=a+1` → `b=3`; then `a=b+1` → `a=4`. Call `f(4,3)` = `-1` → output **`-1 3`**.
* **Both answers are consistent with the C language.** Lesson: write arguments so the result does **not** depend on evaluation order, i.e. **side-effect free**:
```c
a = b + 1;  b = a + 1;  a = f(a, b);      /* now deterministic */
```
* **Pure expressions** (no side effects): `a - b*c/d`, `f(f(a,b), f(f(a,b),a))` (if `f` is pure).
* **Expressions with side effects**: `a = a+1`, `f(a=b+1, b=a+1)`, `i++`.

### ⚠️ Traps
* `!` has **higher** precedence than `&&` and `||`: `!a && b` means `(!a) && b`.
* `!` has **lower** precedence than relational operators: `!a < b` means `(!a) < b`.
* `&&`/`||` have **lower** precedence than relational operators, so `a <= b && b >= c` is `(a<=b) && (b>=c)` — this is exactly the slide's example.
* Bitwise `&` on booleans still *works* by accident for single bits but does **not** short-circuit.
* `5 & 3` = `1` (bitwise), but `5 && 3` = `1` (logical).

### Quick Recall — output-question evaluation checklist
1. Parentheses, innermost first.
2. Unary: `!`, unary `-`, `++`/`--`, `&`, `*`, casts, `sizeof` (right-to-left).
3. `*` `/` `%` (left-to-right).
4. `+` `-` (left-to-right).
5. `<` `<=` `>` `>=`, then `==` `!=`.
6. `&&`, then `||`.
7. `?:`, then `=` (right-to-left).
8. `,`.
9. Track **side effects** separately — and if the same variable is modified twice between sequence points, stop and answer "undefined".

---

## 5. Conditionals: `if`, `if-else`, comparison operators, `switch`

### Concept Summary
* Any **non-zero** value is **TRUE**; the value `0` is **FALSE**. There is no separate boolean type used in this course.
* Comparison (relational/equality) operators **return an `int`**: `1` for true, `0` for false. `4 >= 2` is `1`.

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `<` | less than | `3 < 5` | 1 |
| `<=` | less than or equal | `5 <= 5` | 1 |
| `>` | greater than | `4 > 3` | 1 |
| `>=` | greater than or equal | `4 >= 2` | 1 |
| `==` | equal to | `4 == 4` | 1 |
| `!=` | not equal to | `4 != 4` | 0 |

### General forms (write the evaluation order in the exam)
```c
if (expression) statement1                       /* if */
if (expression) statement1 else statement2       /* if-else */
```
* **`if-else`:** the expression is evaluated. If **non-zero**, `statement1` runs and control passes to the statement **after** `statement2` (i.e. the `else` part is skipped). If it is **0**, `statement2` runs and control passes to the statement after the whole `if-else`.
* **`if` (no else):** if true, `statement1` runs **and then `statement2`**; if false, **only `statement2`** runs.
* `statement1`/`statement2` may be **blocks** `{ }` and may contain further `if`/`if-else` — this is the basis for nested conditions.

### Worked examples from the slides
```c
/* minimum of two integers */
scanf("%d%d", &x, &y);
if (x < y) printf("%d", x);
else       printf("%d", y);

/* acute-angled triangle — a,b,c with c the largest side */
if ((a*a + b*b) > (c*c)) printf("ACUTE\n");
else                     printf("NOT ACUTE\n");

/* is the input zero? */
if (a == 0) printf("Input is 0");
else        printf("Input is non-zero");
```

### `switch`-`case` statement
```c
switch (expression) {
    case constant1: statement1; break;
    case constant2: statement2; break;
    ...
    default:        statementN; break;
}
```
Rules (each one is a possible MCQ):
* The `switch` expression must be of **integer type** — `int` or `char`. **`float`, `double` and strings are NOT allowed.**
* Case labels must be **constant expressions** and must be **unique**.
* Execution **begins at the matching case** and **continues until the end of the switch block or a `break`**.
* If `break` is absent, control **falls through** and executes the following cases too.
* `default` is executed when **no case matches**; usually placed last; its `break` is optional but recommended.
* `break` exits only the nearest `switch`/loop.

```c
/* day suffix: 1st, 2nd, 3rd, 4th … 11th, 12th, 13th … 21st */
char *suffix(int date) {
    char str[3];
    if (date / 10 == 1) return "th";        /* 10..19 all take "th" */
    switch (date % 10) {
        case 1:  strcpy(str, "st"); break;
        case 2:  strcpy(str, "nd"); break;
        case 3:  strcpy(str, "rd"); break;
        default: strcpy(str, "th"); break;
    }
    return str;      /* ⚠ returns a LOCAL array -> dangling pointer */
}
```
* **Fall-through illustration:** with all the `break`s removed and `date%10 == 2`, the code would execute `strcpy(str,"nd"); strcpy(str,"rd"); strcpy(str,"th");` — usually not what you want.

### ⚠️ Traps
* `if (a = b)` assigns and is true whenever `b` is non-zero — the classic "find the error" question.
* `==` binds **looser** than `<`, so `a < b == c` means `(a < b) == c`.
* **Dangling else:** in `if (a) if (b) s1; else s2;` the `else` attaches to the **nearest** `if` (i.e. `if (b)`), not to `if (a)`.
* Omitting braces when there are two statements: only the **first** is controlled by the `if` — the second always runs.
* `if (a == b == c)` compares `(a==b)` with `c` — almost never intended.
* `switch` needs **braces** `{ }` around the cases, and the colon after each case label is mandatory.
* Nesting depth: you may nest `if`s to any depth, but remember the **dangling-else** rule when you do.

### Quick Recall
* Comparison result type: **`int`**, values **0 or 1**.
* `0` = FALSE, **anything else** = TRUE (so `-1` is TRUE!).
* `default` is optional; `break` is what separates cases.

---

## 6. Loops: `while`, `do-while`, `for`, `break`, `continue`

### Concept Summary
| Loop | Test position | Minimum iterations | Semicolon rule |
|---|---|---|---|
| `while (expr) stmt` | **before** the body | **0** | after `stmt` only |
| `do stmt while (expr);` | **after** the body | **1** | **required after `while(expr)`** |
| `for (init; cond; upd) stmt` | before body | 0 | after `stmt` only |

### General forms
```c
while (expression)            /* eval expr; if TRUE run stmt and repeat; if FALSE go after stmt */
    statement;

do                            /* run stmt; then eval expr; TRUE -> repeat, FALSE -> exit */
    statement;
while (expression);           /* <-- semicolon is part of the syntax */

for (i = 0; i < n; i = i + 1) /* init; test; update — all three may be empty */
    statement;
```
* `for (i=0; i<n; i=i+1) stmt;` is **exactly equivalent** to `i=0; while (i<n) { stmt; i=i+1; }`
* `while` and `do-while` are **equally expressive** — anything one can do, the other can.
* `for (;;)` is an **infinite loop**; so is `while (1)`.

### `break` vs `continue`
| Statement | Effect |
|---|---|
| `break;` | Immediately **exit the nearest enclosing loop or switch**. |
| `continue;` | Skip the rest of **this iteration** and go to the next iteration's test/update. |

```c
/* continue: print Pythagorean triplets among consecutive positives, skipping non-positives */
for (i = 0; i < n; i = i + 1) {
    scanf("%d", &curr);
    if (curr <= 0) { continue; }             /* skip negatives and zero */
    if (count == 0)      { pprev = curr; count = 1; }
    else if (count == 1) { prev  = curr; count = 2; }
    else {
        if (pprev*pprev + prev*prev == curr*curr)
            printf("%d %d %d\n", pprev, prev, curr);   /* e.g. 3 4 5 */
        pprev = prev; prev = curr;
    }
}
```
> Input `8 1 -1 3 -3 4 -4 -5 5` → output **`3 4 5`**. (Note: in the slide version `count` stays 2 after the first two positives.)

### Loop invariant (from the slides)
* A **loop invariant** is a property relating the values of variables that **holds at the beginning of every iteration**.
* It is the standard way to argue a loop is **correct**.
```c
s = 0; scanf("%d", &a);
/* Invariant: s holds the sum of all values read, except the last one */
while (!(a == -1)) { s = s + a; scanf("%d", &a); }
```
* If the invariant is true, then at termination (when `-1` is read) `s` is the correct sum.

### Worked trace: GCD with `while` (Euclid)
```c
int a, b, t, g;
scanf("%d%d", &a, &b);
if (b > a) { t = a; a = b; b = t; }      /* ensure a >= b */
while (!(b == 0)) { g = a % b; a = b; b = g; }
printf("%d", a);                          /* gcd */
```
* Key idea: `gcd(a,b) = gcd(b, a % b)`, and `gcd(a,0) = a`.
* `gcd(8,6)`: `8%6=2`, `6%2=0` → **2**. `gcd(102,21)`: `102%21=18`, `21%18=3`, `18%3=0` → **3**.

### Worked trace: longest contiguous increasing subsequence
```c
int prev, curr, len = 0, maxlen = 0;
scanf("%d", &prev);
if (prev != -1) {
    len = 1; maxlen = 1;
    scanf("%d", &curr);
    while (curr != -1) {
        if (prev < curr) len = len + 1;                 /* extend */
        else { if (maxlen < len) maxlen = len; len = 1; } /* reset, remembering max */
        prev = curr;                                     /* ALWAYS do this */
        scanf("%d", &curr);
    }
    if (maxlen < len) maxlen = len;   /* the LAST subsequence may be the longest */
}
```
* Input `9 2 4 0 3 4 6 9 2 -1` → subsequences `9`, `2 4`, `0 3 4 6 9`, `2` → **maxlen = 5**.
* Input `3 2 1 3 5 -1` → **maxlen = 3**.

### Worked trace: matrix trace with nested `for`
```c
float trace = 0.0, a;
scanf("%d", &n);
for (i = 0; i < n; i = i + 1)
    for (j = 0; j < n; j = j + 1) {
        scanf("%f", &a);
        if (i == j) trace = trace + a;   /* diagonal only */
    }
```
* The inner loop runs **n times for each of n rows ⇒ n² reads**.
* Input `3 / 2 0 -1 / 1 3 4 / -1 0 -1` → diagonal `2 + 3 + (-1)` → **trace = 4.0**.

### Loop-count quick formulas (memorise)
| Loop | Iterations |
|---|---|
| `for (i=0; i<n; i++)` | `n` |
| `for (i=1; i<=n; i++)` | `n` |
| nested `n × n` | `n²` |
| right triangle of stars | `1+2+…+n = n(n+1)/2` items |
| bubble sort comparisons | `n(n-1)/2` |
| binary search steps | `≈ log₂ n` |
| `while (n-- > 0)` | `n` times (n decremented to 0) |
| `for (i=0; i<n; i=i+2)` | `⌈n/2⌉` |

### ⚠️ Traps
* Missing `;` after `do { } while (expr)` — compile error.
* `while (i < n);` — the **stray semicolon** makes the loop body empty (infinite loop).
* Forgetting the `i = i + 1` update inside a `while` → infinite loop (a classic "find the error").
* `continue` inside a `while` **skips the update statement** if the update is written at the bottom of the body → infinite loop.
* `break` inside nested loops exits only the **inner** loop.
* `for (i = 0; i < n; i++); printf(...)` — the `printf` is outside the loop because of the stray `;`.
* `float` as a loop counter (`for (f=0.0; f<1.0; f=f+0.1)`) is unreliable — never used in the slides; avoid.

### Quick Recall
* `do-while` = the only loop guaranteed to execute its body **at least once**.
* `break`/`continue` never take an argument and never need braces.

---


## 7. Functions — anatomy, calls, scope and the stack

### Concept Summary
* A **function** groups a task into a named block that can be called from anywhere. It replaces all statements on a flowchart page.
* **Anatomy** of a function definition:
```c
int gcd(int a, int b)   /* <-- function template / interface (header) */
{                       /* formal parameters: a, b                     */
    int t;              /* local variable                            */
    ...
    return a;           /* return statement                          */
}                       /* function body                             */
```
| Part | Meaning |
|---|---|
| `int` before the name | **return type** |
| `gcd` | **function name** |
| `(int a, int b)` | **formal parameters** (with their types) |
| `{ ... }` | **function body** (definition) |
| `return expr;` | the **only mechanism** for returning a value |

* Three related things, commonly confused in fill-in-the-blank:
  1. **Prototype / forward declaration** — `int gcd(int a, int b);` (declares the *interface*, no body).
  2. **Definition** — the prototype **plus** the body.
  3. **Call** — `g = gcd(a, b);`

### Parameter passing (call mechanism — a guaranteed MCQ topic)
* **Values are copied** from the **actual parameters** (at the call site) to the **formal parameters**, **in sequence**.
* Each actual parameter is **converted to the formal parameter's type** if the types differ.
* The function is then executed; the **value of the returned expression** is sent back to the caller.
* ⇒ C is strictly **call by value**. Changing a formal parameter inside the function **never** changes the caller's variable.

### The `return` statement
* `return expr;` returns a value **and immediately exits** the function, transferring control to the **return address** in the caller.
* If the type of `expr` differs from the return type, the value is **converted to the return type**.
* `return;` with **no expression**: the function returns, but the **return value is unpredictable (garbage)**.
```c
float f(int a, float b) { float t = a + b; return; }   /* garbage! */
printf("%d\n", f(a,b));                                 /* unpredictable */
```
* `return` may be used in `main()`; it makes `main` return, which **terminates the program**.
* The **return value may be ignored** — this is legal: `f(y, x);`. We still call the function because functions can have **side effects** (e.g. `scanf` assigns input to a variable).

### Scope and lifetime (memorise the wording)
* **Formal parameters and local variables are visible and accessible only within the function.**
* Memory for them is **allocated only when the function is called** and **freed as soon as the function returns** (exception: `static` variables).
* Therefore two functions may use the same variable name without clashing — think of them as `main.a` and `f.a`.
```c
int f(int a, int b) { return a + b; }
main() { int a = 1, b = 2;  a = f(a,b);  printf("%d  %d", a, b); }   /* 3  2 */
```
* Here `f`'s `a`,`b` are copies; changing them would **not** affect `main`'s `a`,`b`.
* **Nested call:** `a = f(f(a,b), b);` → evaluate the inner call first: `f(1,2)=3`, then `f(3,2)=5` → prints **`5  2`**.

### The **stack** (from the "Stack" lecture)
* A **stack** is a part of memory that **grows in one direction only**.
* The memory of **formal parameters, local variables, the return address and the return value** all live on the stack — one **stack frame** (activation record) per active call.
* Each call pushes a new frame; when the call returns, its frame is **erased**.
* Stack depth = number of **pending (unfinished) calls**.

### ⚠️ Traps — favourite "find the error" items
* **The exchange bug** seen in the slides: `if (a < b) { t = a; a = b; b = a; }` — the last line must be **`b = t;`**. As written, `b` gets `a`'s *new* value, so the swap fails.
* Forgetting `return` in a function that promises a value → garbage.
* Calling a function **before** declaring it (no prototype and defined below `main`) is not allowed in modern C.
* `return` inside a loop returns from the **function**, not just from the loop. (Use `break` for the loop.)
* Assigning a `float` to an `int` return type silently truncates.
* The return value's type is the **declared** return type, not the type of the expression.

### Quick Recall
* `return expr;` = only way to send a value back.
* Arguments are copied **in sequence**, converted to the formal types.
* Locals exist only during the call; the stack frame is erased on return.

---

## 7b. Functions that change the caller: pointers, designing functions

### Call by value means changes are lost
```c
void swap(int a, int b) { int t;  t = a;  a = b;  b = t;
    printf("From swap a = %d b = %d\n", a, b); }
int main() { int a = 1, b = 2;  swap(a, b);
    printf("From main a = %d b = %d\n", a, b); }
/* Output:
   From swap a = 2 b = 1
   From main a = 1 b = 2      <-- main is UNCHANGED */
```
* Passing `int`/`float`/`char` as parameters does **not** allow passing anything "back" to the calling function. Any changes are **lost** when the function returns.

### The fix: pass pointers
```c
void swap(int *ptra, int *ptrb) {
    int t;
    t     = *ptra;
    *ptra = *ptrb;
    *ptrb = t;
}
int main() { int a = 1, b = 2;  swap(&a, &b); }   /* pass ADDRESSES */
```
* The formals are **`int *`** (pointers to int); the call passes **`&a`, `&b`**.
* Tracing: `ptra` holds the address of `a`, `ptrb` the address of `b`. `*ptra` names **a's box**, so writing `*ptra = *ptrb` really changes `a`. Output: main's `a = 2, b = 1`.

### ⚠️ The pointer-swap trap (homework from the slides)
```c
void swap(int *ptra, int *ptrb) {
    int *ptrt;
    ptrt = ptra;  ptra = ptrb;  ptrb = ptrt;   /* swaps the LOCAL POINTERS only */
}
```
* This does **NOT** swap the caller's values. It only rearranges the two local pointer variables, which are themselves copies. The values `*ptra`, `*ptrb` are never touched. **Answer to "does it swap correctly?": No.**

### Designing programs with functions
* **General principle:** break the task into sub-tasks, and those into smaller sub-tasks, until each sub-task is easily solvable in a function. Write **one function per sub-task**.
* **Design top-down** (big task → small tasks). **Debug/test bottom-up** (test the elementary functions first, then the bigger ones).
* A function should be **small, single-purpose and reusable** — `gcd` is reused to build `totient`, which is reused to build `isprime`.

```c
int gcd(int a, int b) {            /* corrected exchange */
    int t;
    if (a < b) { t = a;  a = b;  b = t; }
    while (!(b == 0)) { t = b;  b = a % b;  a = t; }
    return a;
}
int totient(int n) {               /* count of 1<=k<n with gcd(n,k)==1 */
    int i, tot = 1;
    for (i = 2; i < n; i++)
        if (gcd(n, i) == 1) tot = tot + 1;
    return tot;
}
int isprime(int n) {               /* n is prime iff it is co-prime to 1..n-1 */
    if (totient(n) == n - 1) return 1;
    else                     return 0;
}
```

### Building larger computations — "n choose k"
```c
int fact(int r) {                  /* r! */
    int i, ans = 1;
    for (i = 0; i < r; i = i + 1) ans = ans * (i + 1);
    return ans;
}
main() {
    int n, k, res, t1, t2, t3;
    scanf("%d%d", &n, &k);
    t1 = fact(n);  t2 = fact(k);  t3 = fact(n - k);
    res = (t1 / t2) / t3;
    printf("%d choose %d is %d\n", n, k, res);   /* 4 choose 2 is 6 */
}
```
* Each `fact` call pushes a **fresh stack frame** (params, locals, return address, return value). When `fact` returns, its frame is **erased** and the returned value is copied into the caller's box.
* Careful: `(t1/t2)/t3` performs **integer** division at each step; `(n!)/(k!)/((n-k)!)` is only valid because the intermediate values happen to divide exactly.
* The slide version `printf("%d choose %d is");` with **no arguments** prints garbage values — a classic find-the-error question (arguments missing).

### ⚠️ Traps
* To modify a caller's variable, the formal parameter must be a **pointer** and the call must pass an **address** (`&x`).
* Changing a *pointer parameter itself* (not `*p`) has no effect outside the function.
* `main()`'s return type: write `int main()` and `return 0;`. (The slides also use plain `main()`.)
* A function must be **declared/defined before it is used**, or you need a **prototype** above.
* Ignoring a return value is legal but pointless unless the function has **side effects**.

### Quick Recall
* **Call by value** = copies; **emulate call by reference** with pointers.
* `void` return type ⇒ no value; a `return;` just exits.
* Design **top-down**, debug **bottom-up**.

---

## 8. Arrays

### Concept Summary
* An **array** is a **consecutively allocated group of variables of the same type, whose names are indexed**. Definition:
```c
int   num[10];      /* 10 int boxes: num[0] .. num[9]   */
float w[100];       /* 100 float boxes                  */
char  s[10];        /* 10 char boxes                    */
double mat[5][6];   /* 2-D array: 5 rows x 6 columns    */
```
* **Indices always start at 0 in C.** The last valid index of `a[n]` is **`a[n-1]`**.
* An array definition creates **two things**: (i) the consecutive boxes, and (ii) a **box with the same name as the array that holds the address of the base (first) element**. So `int num[10]` gives **11** boxes: 10 `int` + 1 address-of-int.
* There is **no bounds checking** — `a[10]` in a 10-element array is not caught by the compiler; it is **undefined behaviour**.

### Size rules
* The size must be a **constant expression**: `float w[10*10];` is fine.
* A **variable** as a size (`int size; float w[size];`) is **not allowed in ANSI C**; it is allowed in **C99 and later**. The slides say: *avoid this feature*.
* Total size in bytes = `n * sizeof(element)`: `int num[10]` is `10*4 = 40` bytes.

### Initialisation rules (very heavily tested)
```c
int num[]  = {-2, 3, 5, -7, 19, 103, 11};   /* size = 7, taken from the list  */
int num[10]= {-2, 3, 5, -7, 19, 103, 11};   /* rest (num[7]..num[9]) become 0 */
int num[100] = {0, -1, 1, -1};              /* first 4 as given, rest 0       */
int num[6] = {-2, 3, 5, -7, 19, 103, 11};   /* ERROR: 7 values for size 6     */
```
1. Values are placed within **curly braces**, separated by commas.
2. If the size is **unspecified**, it is set to the **number of initial values**.
3. Elements are assigned **in index order**: first constant → `[0]`, second → `[1]`, …
4. Any **remaining** elements are set to **0** (`0.0` for float/double, `'\0'` for char).
5. **The number of initial values must be ≤ the specified size.**
6. Initial values may be constants, **constant expressions** (`7*25*1023 + '1'`) or simple expressions of constants. Types are promoted/demoted: `int num[] = {1.09, 'A', 25.05};` truncates the floats to `1`, `65`, `25`.
```c
int curr = 5;
int num[] = { 2, curr*curr + 5 };   /* allowed in ANSI C for "simple" expressions */
```

### Reading and writing
```c
/* read directly into an array element */
int num[10], n, i;
scanf("%d", &n);
for (i = 0; i < n && i < 10; i = i + 1)
    scanf("%d", &num[i]);         /* &num[i] means &(num[i]), NOT (&num)[i] */
```
* `&num[i]` is made of two operators: `[ ]` (array indexing) and `&` (address-of). **`[ ]` has higher precedence than `&`**, so `&num[i]` = `&(num[i])`.
* For a `char` array use `scanf("%c", &s[j])`; for strings `scanf("%s", s)` (no `&`).

### Arrays and pointers
* The **array name is a pointer to the first entry**: `num` ≡ `&num[0]`.
* `a[i]` is **exactly equivalent** to `*(a+i)`.
* The type of `num` is `int[]`, but internally C represents `num` and a `int *` the same way — so **`int *` can be used wherever `int[]` can be**.

### Classic array programs from the slides
```c
/* read at most 100 chars and print them in reverse */
char s[100]; int count = 0, ch, i;
ch = getchar();
while (ch != EOF && count < 100) { s[count] = ch; count = count + 1; ch = getchar(); }
i = count - 1;
while (i >= 0) { putchar(s[i]); i = i - 1; }

/* reverse an array IN PLACE using two moving pointers */
void rev_array(int a[], int n) {
    int *b = a + n - 1;                  /* last element */
    while (b > a) { swap(a, b); a = a + 1; b = b - 1; }
}
void swap(int *ptra, int *ptrb) { int t = *ptra; *ptra = *ptrb; *ptrb = t; }
```
* Note: after the first `a = a + 1`, the parameter `a` no longer points to the base — this is fine here because the caller's array is modified through the pointers.

### ⚠️ Traps
* `a[n]` (out of bounds) is **undefined** — a classic "what happens?" question.
* `int num[6] = {7 values}` → **compile error**.
* `sizeof(a)` on an array gives the **total bytes**, but `sizeof(a)` inside a function that received `int a[]` gives the **pointer size** (8), not the array size. This is a very common MCQ.
* An array **cannot be assigned** as a whole: `b = a;` is illegal; you must copy element by element.
* An array **cannot be returned** from a function; return a pointer instead.
* `int a[10]; a[10] = 0;` writes past the end.

### Quick Recall
* `n` elements ⇒ valid indices `0 … n-1`.
* Unspecified size ⇒ taken from the initialiser list; leftover elements ⇒ **0**.
* `a[i]` ≡ `*(a+i)`; the array name **decays** to a pointer to the first element.

---

## 9. Strings & character arrays

### Concept Summary
* A **string** is a sequence of characters **terminated by `'\0'`** (the **NULL character**, ASCII 0). The `'\0'` is **not part of the string** — it is the terminator.
* Two ways to initialise a "message":
```c
char s[] = {'I',' ','a','m',' ','D','O','N','\0'};   /* explicit chars + terminator */
char s[] = "I am DON";                               /* string constant — '\0' added AUTOMATICALLY */
```
* **String constants** are written in **double quotes**: `"I am a string"`.
* Character constants are written in **single quotes**: `'A'`.

### Printing and reading
```c
printf("%s", "I am DON");     /* I am DON       — %s is the string conversion */
printf("%s", str);            /* prints up to (not including) the first '\0' */
putchar(str[i]);              /* prints ONE character, ignores '\0' meaning */
scanf("%s", str);             /* reads a whitespace-delimited word — NO & needed */
scanf("%c", &ch);             /* reads ONE character (does not skip whitespace) */
```

### The `'\0'` behaviour — a favourite output question
```c
char str[] = "I am GR8DON";
printf("%s", str);                 /* I am GR8DON            */
str[4] = '\0';
printf("%s", str);                 /* I am                   */
int i; for (i = 0; i < 11; i++) putchar(str[i]);   /* I amGR8DON  */
```
* `%s` stops at the **first `'\0'`**.
* The characters **after** the `'\0'` are **not lost** — they are still in memory. They were simply not printed because `%s` stopped.
* The `putchar` loop prints all 11 characters, including the `'\0'` (which usually displays as nothing, but may show oddly depending on terminal settings).

### Strings and the string library (`<string.h>`)
| Function | Prototype | Purpose |
|---|---|---|
| `strlen` | `size_t strlen(const char *s)` | number of chars **before** `'\0'` |
| `strcpy` | `char *strcpy(char *d, const char *s)` | copy including `'\0'` |
| `strcmp` | `int strcmp(const char *a, const char *b)` | 0 if equal, <0 / >0 otherwise |
| `strcat` | `char *strcat(char *d, const char *s)` | append |
| `strchr` | `char *strchr(const char *s, int c)` | find character |

* `strlen("I am DON")` = **8** — the terminator is **not counted**.
* An array big enough for a string of length `len` needs **`len + 1`** bytes.
* `strcmp` returns **0** for equal strings (so `if (strcmp(a,b) == 0)`), never use `==` on strings.

### Duplicating a string on the heap (slide example)
```c
char *duplicate(char *s) {
    int i = 0, len;
    char *t;
    for (i = 0; s[i] != '\0'; i++) ;     /* find length */
    len = i;
    t = (char *) malloc((len + 1) * sizeof(char));   /* +1 for '\0' */
    for (i = 0; i < len; i++) t[i] = s[i];
    t[i] = '\0';
    return t;                            /* safe: t is on the HEAP, not the stack */
}
int main() { char s[] = "Sample"; char *t = duplicate(s); printf("%s\n", t); }
```

### Character arrays and `char *`
* `char s[10]` — a **writable** array of 10 characters; you may change `s[i]`.
* `char *s = "hello";` — `s` points at a **string literal**, which is typically **read-only**; `s[0] = 'H'` is undefined behaviour.
* `char *mnth[12]` — an **array of pointers** to strings (each row may have a different length).
* `char mnth[][7]` — a **2-D char array** (all rows the same length, 7 including the terminator).

### ⚠️ Traps
* `'A'` (char) vs `"A"` (a 2-byte string `'A'`,`'\0'`) — different types.
* `printf("%c", "A")` and `printf("%s", 'A')` are both wrong.
* Forgetting the `'\0'` when building a string by hand → `%s` runs off the end (undefined).
* Forgetting to allocate `len+1` bytes → off-by-one, a classic error.
* `strlen(s)` is called **repeatedly** inside a loop condition → slow (a performance MCQ).
* Declaring `char s[5] = "hello";` → too small for `"hello\0"` (6 bytes needed).
* Returning a `char str[3]` from a function (`suffix` example) returns a **dangling pointer**.

### Quick Recall
* String = character array + **`'\0'` terminator**.
* `strlen` **excludes** `'\0'`; `sizeof` **includes** it.
* `%s` prints until the first `'\0'`; `%c` prints one character.

---

## 10. Pointers — addresses, dereferencing, arithmetic, `sizeof`

### Concept Summary
* A **pointer is a variable that contains the address of another variable**. We say the pointer **"points to"** that variable.
* Two fundamental operators:
  * **`&`** — the **address-of** operator: `&x` gives the location of the box `x`. It can be applied to **any defined variable**.
  * **`*`** — the **dereference** operator: `*p` gives the **content of the variable that `p` points to**.
* Because "the address of a box" is itself a piece of data, it must be stored in a box of the right type: **address of an `int`** is written **`int *`**.

```c
int num[10];
int *ptr;              /* ptr is "pointer to int" — a NEW box of an address type */
ptr = &num[1];         /* ptr now points to num[1] */
*ptr = 7;              /* same effect as num[1] = 7 */
scanf("%d", ptr);      /* reads an integer INTO the box pointed to by ptr (= num[1]) */
```
* Because the array name `num` already holds the address of `num[0]`, we have **`num == &num[0]`**.
* In C, **`num` and `ptr` are represented the same way internally**, so **`int *` can be used wherever `int[]` can be used**.

### The three things you can do with a pointer
1. **De-reference** it: `*p`, `p[0]`.
2. **Pointer arithmetic**: `p + 1`, `p - 1`, `p++`, `p--`, and subtraction of two pointers.
3. **Compare** pointers: `==`, `!=` always; `<`, `<=`, `>`, `>=` **only if they point into the same array**.

### Pointer arithmetic — the key formula
> **`ptr + i` is the byte address `ptr + i * sizeof(type)`.**

| Declaration | `ptr + 1` advances by |
|---|---|
| `char *ptr` | **1 byte** |
| `int *ptr` | **4 bytes** |
| `float *ptr` | 4 bytes |
| `double *ptr` | 8 bytes |

* **This is exactly why C arrays start at index 0!** It makes `a[i] == *(a + i)` work out.
* Example from the slides: `int a[10]` starting at byte `0x2000`. Then
  `a[2] = *(a+2)` is at byte `a + 2*sizeof(int) = 0x2000 + 8 = 0x2008`.
  For `char s[8]` the cells are **1 byte apart**; for `int a[4]` they are **4 bytes apart**.
* **Subtracting two pointers** gives the **number of elements** between them (not bytes).

### `sizeof` operator
* `sizeof` gives **the number of bytes occupied by a value of a type**. It is an **operator**, not a function.
* Typical values: `sizeof(int)` = 4, `sizeof(float)` = 4, `sizeof(char)` = 1, `sizeof(double)` = 8, `sizeof(pointer)` = 8.
* Three usages:
```c
sizeof(expression)   /* size of the type of the expression, e.g. sizeof(10) == sizeof(int) */
sizeof(typename)     /* e.g. sizeof(int) == 4 */
sizeof(array)        /* total bytes: for int num[10] it is 40 == 10*sizeof(int) */
```
* Common idioms: number of elements = `sizeof(a)/sizeof(a[0])`; allocating an array = `malloc(n * sizeof(int))`.

### ⚠️ Traps
* `&` and `*` are inverses: `*&x` is `x`. `&*p` is `p`.
* Comparing pointers with `<` that do **not** point into the same array is **undefined**.
* `sizeof(a)` inside a function where the parameter is `int a[]` gives the **pointer size (8)**, not the array size — arrays decay when passed.
* `p + 1` does **not** add 1 byte for an `int *`; it adds 4. This is the #1 pointer-arithmetic MCQ.
* Dereferencing an **uninitialised** or **NULL** pointer crashes / is undefined.
* `int *p; *p = 5;` — writing through an uninitialised pointer is undefined (there is no box to write to).

### Quick Recall
* `&x` → address of `x`; `*p` → the value stored at the address in `p`.
* `a[i]` ≡ `*(a + i)` ≡ `*(&a[0] + i)`.
* `sizeof` is used **in pointer arithmetic** and in `malloc`; it counts **bytes**, `strlen` counts **characters**.

---

## 10b. Passing arrays & subarrays, the heap (`malloc`/`free`), dangling pointers

### Passing arrays to functions
* When you pass an array, what is really copied is the **address of the first element** — so the function can **modify the caller's array**.
* The formal parameter may be written `int a[]` or `int *a`; they mean the same thing.
* The **size must be passed separately** — the function cannot know the length of the array.
```c
/* read input into a char array until Ctrl-D or the array is full */
int read_into_array(char s[], int max) {
    int count = 0, ch;
    ch = getchar();
    while (ch != EOF && count < max) { s[count] = ch; count++; ch = getchar(); }
    return count;                     /* return the count — the caller needs it */
}
```
* Therefore a function **cannot** compute `n = sizeof(a)/sizeof(a[0])` for its array parameter.

### Passing a SUBARRAY (`f + i`)
```c
int copy_array(int a[], int b[], int n) {
    int i;
    for (i = 0; i < n; i = i + 1) b[i] = a[i];
    return 0;
}
/* copy n numbers from f[] starting at index i, to t[] starting at index j */
int copy_array_2(int f[], int i, int t[], int j, int n) {
    copy_array(f + i, t + j, n);      /* <-- pass a SUBARRAY by pointer arithmetic */
    return 0;
}
```
* `a` becomes the array `(f+i)[]` starting at `f[i]`, and `b` becomes `(t+j)[]` starting at `t[j]`.
* Inside, `b[i] = a[i]` is `*(b+i) = *(a+i)`; since `b` is `t+j`, `b[i]` is `(t+j)[i]` = `t[j+i]`. **That is exactly the required `t[j+i] = f[i+j]`.**
* A single memory cell has **many names**: `f[3]`, `*(f+3)`, `(f+2)[1]`, `(f+1)[2]` are all the same box.

### Why `b = a;` does not copy an array
* It only makes `b` point to `a`'s first element. Element-by-element copying (or `memcpy`) is required.
* Similarly, **arrays cannot be returned** from functions — return a pointer instead.

### Dangling pointers (top UB question)
```c
int *increment(int n) {
    int temp;                 /* LOCAL — erased when the function returns */
    int *ptr = &temp;
    temp = n + 1;
    return ptr;               /* returns the address of a DEAD box */
}
```
* **Anything allocated for the called function on the stack is erased as soon as it returns.** The returned address therefore points to nothing valid — a **dangling pointer**.
* Using it is **undefined behaviour** (it may appear to work, then fail).

### The heap: `malloc` and `free` (`<stdlib.h>`)
* The **heap** is a **globally accessible pool of memory** that is **not erased** when a function returns.
* `malloc(n)` allocates **`n` bytes** on the heap and returns a pointer (castable to any type). It returns **`NULL`** if it cannot allocate.
* `calloc(n, size)` allocates and **zero-initialises**.
* `free(ptr)` releases memory previously allocated on the heap. After freeing, set the pointer to `NULL` to avoid accidental re-use.
```c
#include <stdlib.h>
int *ptr = (int *) malloc(10 * sizeof(int));   /* 10 ints on the heap */
free(ptr);
ptr = NULL;
```
* Correct fix for the dangling-pointer problem:
```c
int *increment(int n) {
    int *ptr = (int *) malloc(sizeof(int));
    *ptr = n + 1;
    return ptr;                     /* safe: the box is on the HEAP */
}
int main() { int *p = increment(1); printf("%d\n", *p);  free(p);  p = NULL; }
/* Output: 2 */
```

### Common errors with `malloc`/`free` (memorise this list)
1. **Forgetting to `malloc`** — writing through an uninitialised pointer.
2. **Not allocating enough space** — e.g. `len` characters instead of **`len+1`** (forgot the `'\0'`).
3. **Forgetting to `free`** after use → **memory leak**.
4. **Freeing the same memory more than once** → **runtime error**.
5. Using a pointer **after** it has been freed (use-after-free) → undefined.
6. Not checking `malloc`'s result for `NULL`.

### ⚠️ Traps
* "Return a pointer to a local variable" is **always wrong**; return a pointer to heap memory (or write into an array passed by the caller).
* `free(NULL)` is safe — it does nothing. `free` twice on the same non-null pointer is a runtime error.
* `sizeof(int) * 10` and `10 * sizeof(int)` are the same; `malloc(10)` alone gives only **10 bytes**, enough for 2 ints, not 10.
* An array *created with `malloc`* must be freed; a static/local array must **not** be freed.

### Quick Recall
* Use the **heap** when a value must outlive the function that created it.
* `malloc` → heap, `free` → release, `NULL` → "points nowhere".
* Subarray = `array + offset`.

---

## 11. Recursion

### Concept Summary
* **Recursion** = a function **calls itself**. Every correct recursive function needs:
  1. One or more **base cases** (no further call), and
  2. A **recursive case** that makes progress toward a base case.
* **Design rule from the slides:** *think recursively — not in terms of the stack*. The stack is only used by the machine for **execution and tracing**.
* **Depth of recursion** = the maximum size of the stack = the maximum number of **pending (unfinished) function calls**.
* **Memory used by a recursive program** = local memory + **stack depth**.
* Recursion is the natural way to express "do the same job on a smaller input".

### Linear recursion
```c
/* factorial */
int fact(int n) {                       /* assumes n >= 0 */
    if (n == 0) return 1;               /* base case */
    else        return n * fact(n-1);   /* recursive case: smaller input */
}

/* Euclid's gcd, recursively */
int gcd(int a, int b) {
    if (b == 0) return a;
    else        return gcd(b, a % b);
}

/* reverse the first n elements of a[], IN PLACE */
void reverse(int a[], int n) {
    if (n == 0 || n == 1) return;       /* nothing to reverse */
    int t = a[0]; a[0] = a[n-1]; a[n-1] = t;   /* exchange the two ends */
    reverse(a + 1, n - 2);              /* recurse on the middle */
}
```
* Each call adds one frame: **params, locals, return address, return value**. When the innermost base case returns, the frames are **popped one by one** and the values propagate back out.
* `fact(4)` → `4 * fact(3)` → … → `4*3*2*1` = **24**. Depth = 5 pending calls.

### Two-way recursion (divide and conquer)
```c
/* find the maximum of an array — LINEAR recursive version (depth n) */
int max_array(int a[], int n) {
    int maxval;
    if (n == 0) return -99999;        /* some large negative number */
    if (n == 1) return a[0];
    maxval = max_array(a + 1, n - 1); /* max of the rest */
    return max(a[0], maxval);
}

/* find the maximum — TWO-WAY recursive version (depth ~ log n) */
int max_arr(int a[], int n) {
    if (n == 0) return -INFTY;
    if (n == 1) return a[0];
    return max( max_arr(a, n/2),                 /* first half  */
                max_arr(a + n/2, n - n/2) );     /* second half */
}
```
| Version | Stack depth |
|---|---|
| linear `max_array` | **n** |
| two-way `max_arr` | **≈ 1 + log₂ n** |

* The two-way version halves the array each time — the **stack depth is logarithmic**, which is the whole point of asking "can we reduce the stack depth?".

### Two-way recursion is elegant but can be very wasteful
```c
/* Fibonacci: F0=1, F1=1, Fn = Fn-1 + Fn-2 */
int fib(int n) {
    if (n == 0 || n == 1) return 1;
    else return fib(n-2) + fib(n-1);
}
```
* This is a **correct but very inefficient** formulation.
* The call tree for `fib(5)` performs **many duplicate calls** — `fib(2)`, `fib(1)`, `fib(0)` are all computed repeatedly.
* **Number of calls ≈ Fₙ** — exponential growth. Compare with the **iterative** version (`a=b=1; while(n-- > 0){t=a+b; a=b; b=t;}`) which is linear.
* ⇒ **Memoisation** (remembering results) or iteration fixes it.

### Recursive binary search
```c
int binsearch(int a[], int n, int key) {
    int mid, ret_val;
    if (n == 0) return -1;                 /* empty array: not found */
    mid = (n - 1) / 2;
    if (a[mid] == key) return mid;         /* found */
    if (a[mid] > key)                      /* key is in the left half */
        return binsearch(a, mid, key);
    if (a[mid] < key) {                    /* key is in the right half */
        ret_val = binsearch(a + mid + 1, n - mid - 1, key);
        if (ret_val == -1) return -1;
        else return mid + 1 + ret_val;     /* adjust the index for the offset */
    }
}
```
* Requires `a[]` to be **sorted in non-descending order**.
* The `mid + 1 +` adjustment is needed because the right half is passed as a **subarray** starting at `a + mid + 1`.
* Steps ≈ **log₂ n**; compare with linear search's **n** steps.

### Recursion vs iteration
| | Recursion | Iteration |
|---|---|---|
| Code clarity | often clearer for divide-and-conquer | clearer for simple counting |
| Extra memory | **one stack frame per pending call** | none |
| Risk | **stack overflow** for deep recursion | — |
| Speed | slower (call overhead) | faster |
| Classic example | `fib` exponential | `fib` linear |

### ⚠️ Traps
* **Missing base case** → infinite recursion → stack overflow (segmentation fault).
* Base case that does not get reached (wrong "smaller input") → infinite recursion.
* Forgetting to `return` the recursive call's value (`fact(n-1);` instead of `return n*fact(n-1);`) → garbage.
* For two-way recursion, **both** halves must shrink; otherwise you recurse forever.
* Deep recursion on large `n` (e.g. linear `max_array` on 1,000,000 elements) can exhaust the stack even though the answer is correct.

### Quick Recall
* **Base case + smaller input = correct recursion.**
* Depth = number of pending calls; memory = locals + stack depth.
* Linear recursion depth = n; two-way (halving) depth ≈ log₂ n.
* Naïve recursive Fibonacci is **exponential** — a favourite MCQ answer.

---

## 12. Structures

### Concept Summary
* A **structure** is a **collection of variables with a common name**. The variables may be of **different types** (or arrays). The member variables are called **fields** (members).
* Motivation: to create **our own data types** from the built-in ones. A point "having an x co-ordinate and a y co-ordinate" is best modelled as two fields in one type, not as two unrelated variables or a size-2 array.

```c
struct point {          /* this DEFINES A TYPE named "struct point" */
    int x;
    int y;
};                      /* <-- the semicolon after } is mandatory */
```

### Declaring and using structure variables
```c
struct point pt;          /* a variable of type struct point      */
struct point pt1, pt2;    /* several variables                    */
struct point pts[6];      /* an ARRAY of 6 struct point values    */
```
* Access a field with the **dot operator `.`**:
```c
pt.x = 1;
pt.y = 0;
pts[2].x = 7;             /* read as (pts[2]).x */
```
* **`.` and `[]` have the same precedence, associativity left→right**, so `pts[i].x` is `(pts[i]).x` and `pts[i].x` is **not** `(pts[i].x)` — the array index applies first.
* A structure variable can be **assigned as a whole**: `pt1 = pt2;` copies all fields. (Arrays cannot be assigned this way; structures can.)
* Recommended practice (from the slides): **define structs at the beginning of the file, after `#include`**.

### Structures are a type — so they can be used like `int`
```c
struct point make_point(int x, int y) {     /* function RETURNING a structure */
    struct point temp;
    temp.x = x;
    temp.y = y;
    return temp;                            /* the whole structure is returned */
}
int main() {
    int x, y;  struct point pt;
    scanf("%d%d", &x, &y);
    pt = make_point(x, y);
    return 0;
}
```
```c
double norm2(struct point p) {              /* function TAKING a structure */
    return sqrt(p.x * p.x + p.y * p.y);     /* Euclidean norm */
}
```
* **Functions can return structures just like `int`, `char`, `int *` etc., and structures can be passed as parameters.**
* Structure arguments are passed **by value**: the **whole structure is copied** into the formal parameter. (Which is why large structures are usually passed by pointer.)
* `sqrt` lives in the **math library**: include `<math.h>` and compile with **`gcc file.c -lm`**.

### Nested structures (structures inside structures)
```c
struct point { int x; int y; };
struct rect {
    struct point leftbot;
    struct point righttop;
};
struct rect r;
r.leftbot.x  = 0;         /* chain the dot operators */
r.righttop.y = 10;
```
* Each `struct rect` contains **two instances of `struct point`** — so it has 4 integer fields in total.
* The field-access expression is built by **chaining `.`** left to right.

### Pointers to structures and the `->` operator
```c
struct point pt, *p;
p = &pt;
(*p).x = 5;      /* explicit form */
p->x   = 5;      /* PREFERRED shorthand — identical meaning */
```
| Expression | Means |
|---|---|
| `pt.x` | field `x` of the structure `pt` |
| `(*p).x` | field `x` of the structure **pointed to** by `p` |
| `p->x` | **exactly the same** as `(*p).x` |

* `->` combines a **dereference** and a **field selection**: `p->x` ≡ `(*p).x`.
* The `.` operator needs a **structure value** on its left; `->` needs a **pointer** on its left.

### `typedef`
```c
typedef struct dllnode * Ndptr;     /* Ndptr is now a type: pointer to struct dllnode */
typedef struct dllist  * Dllist;    /* Dllist is now a type: pointer to struct dllist  */
struct dllnode { int data; struct dllnode *next; struct dllnode *prev; };
struct dllist  { Ndptr head; Ndptr last; };
```
* `typedef` creates an **alias** for a type — it does not create a new type and does not allocate memory.

### ⚠️ Traps
* Forgetting the final **`;`** after `struct point { ... }` — the most common structure syntax error.
* `struct point` (the type name) vs `point` (a tag, not a type name) — you must write **`struct point`** unless you `typedef` it.
* `p.x` when `p` is a pointer — **compile error**; use `(*p).x` or `p->x`.
* Comparing two structures with `==` is **not allowed**; compare field by field (or use `memcmp`).
* Passing a large structure by value copies the whole thing — expensive.
* `sizeof(struct point)` may be larger than the sum of the field sizes because of **padding** — a good MCQ.

### Quick Recall
* `struct` = a user-defined type grouping different types under one name.
* `.` works on a value; `->` works on a pointer; `p->x` ≡ `(*p).x`.
* Structures **can** be assigned, passed and returned as values; arrays **cannot**. Structures **cannot** be compared with `==`.

---

## 13. Multi-dimensional arrays & C type expressions

### Concept Summary
```c
double mat[5][6];      /* 5 rows, each of 6 columns, each entry a double */
int    mat[5][6];
float  mat[5][6];
```
* `double` = **double precision floating point**. The slides advise: if you do a lot of floating-point computation, **use `double` instead of `float`**.
* The `(i,j)`-th element is written **`mat[i][j]`** — *not* `mat[i,j]`.
* **Row numbering and column numbering each start at 0** (unlike matrix notation in maths).
* Storage is **row-wise (row-major)**: all of row 0, then all of row 1, and so on.

### Reading and printing
```c
void print_matrix(double mat[5][6]) {
    int i, j;
    for (i = 0; i < 5; i = i + 1) {
        for (j = 0; j < 6; j = j + 1)
            printf("%f ", mat[i][j]);
        printf("\n");                        /* newline after each row */
    }
}
void read_matrix(double mat[5][6]) {
    int i, j;
    for (i = 0; i < 5; i = i + 1)
        for (j = 0; j < 6; j = j + 1)
            scanf("%f", &mat[i][j]);         /* &mat[i][j] = &(mat[i][j]) */
}
```
* `&mat[i][j]` needs **no parentheses** because **`[ ]` has higher precedence than `&`**.
* `scanf` with `%f`/`%d` **skips whitespace**, so it does not matter whether the 30 values are given as 5 rows or on one line.

### The parameter rule (heavily tested)
* **You must specify the number of COLUMNS** in the formal parameter: `double mat[5][6]`.
* Changing it to `mat[6][5]` would **not** mean the same thing — the compiler needs the row length to compute `mat[i][j] = *(*(mat+i) + j)`.
* The first dimension may be omitted: `void f(int mat[][6])` is legal; `void f(int mat[][])` is **not**.

### Initialising 2-D arrays
```c
int a[][3] = { {1,2,3},          /* values are given ROW-WISE: first row, then second, ... */
               {4,5,6},
               {7,8,9},
               {0,1,2} };        /* this makes a 4 x 3 matrix */

int a[][3] = { {1}, {2,3}, {3,4,5} };   /* gives  1 0 0 / 2 3 0 / 3 4 5 */
```
Rules:
1. **Values are given row-wise.**
2. **The number of columns must be specified**; the number of rows may be inferred.
3. Each row is enclosed in its own `{ ... }` braces.
4. If a row has **fewer** values than columns, the **remaining columns are set to 0** (`0.0` for double, `'\0'` for char).

### C type expressions — how to read them
```c
int **mat;        /* pointer to a pointer to int — most general */
int *mat[5];      /* an ARRAY of 5 pointers to int  (only the number of ROWS is fixed) */
int (*mat)[5];    /* a POINTER to an array of 5 ints (only the number of COLUMNS is fixed) */
int arr[2][3];    /* both the number of rows and columns are fixed */
```
* Reading rule: `()` and `[]` bind tighter than `*`; start from the name and work outward.
* `int (*mat)[5]` means: *`mat` is an address; if you dereference it (`*mat`) you get an **array of size 5***.
* The correct type to receive a 2-D array in a function is **`int (*mat)[5]`** (or `int mat[][5]`).

### Index equivalences (memorise this table)
| Written as | Equivalent to |
|---|---|
| `mat[0][0]` | `(*mat)[0]` = `*(*mat)` = **`**mat`** |
| `mat[i][j]` | `(*(mat+i))[j]` = **`*(*(mat+i) + j)`** |
| `mat[2][3]` | `(*(mat+2))[3]` = `*(*(mat+2) + 3)` |
| `mat + 1` | pointer to the **2nd row** (an array of 5 ints) |
| `*mat` | the **first row**, an array of size 5 |
| `*(mat + i)` | the **i-th row** |

* **Q (from the slides):** which of these equals `mat[1][1]`?
  * `*(*(mat + 1) + 1)` ✅ (correct)
  * `**mat + 2`  (that is `mat[0][0] + 2`)
  * `*(mat + 1)[1]` ❌ (that is `*((mat+1)[1])`, a different thing)
* **Q:** how do you search for `key` in the **second row** using `int search(int a[], int n, int key)`?
  * `search(mat[1], 5, key)` ✅ — `mat[1]` is an `int *`
  * `search(*(mat+1), 5, key)` ✅ — the same thing
  * `search(mat+1, 5, key)` ❌ — `mat+1` has type `int (*)[5]`, not `int *`

### Array of arrays vs 2-D arrays
| | Array of arrays e.g. `char *mnth[12];` | 2-D array e.g. `double matrix[10][10];` |
|---|---|---|
| Row lengths | may **all be different** (`mnth[6]` is `"July"` = 5, `mnth[8]` is `"September"` = 10) | **all rows the same length** |
| Good for | string/word processing, graphs, non-uniform structures | matrix computation |
| Not good for | matrices | non-uniform structures |

```c
char *mnth[]  = {"Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"};
char mnth[][7]= {"Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"};
```
```c
printf("%s", mnth);          /* Jan     (type char *)  */
printf("%c", **mnth);        /* J       (type char)    */
printf("%s", *(mnth+1));     /* Feb     */
printf("%s", mnth[0]+1);     /* an      */
printf("%c", **(mnth+7));    /* A       */
```
* Here `mnth` has type **`char **`**, `mnth[0]` has type **`char *`**, `mnth[0][0]` has type **`char`**.

### ⚠️ Traps
* `mat[i,j]` — the comma operator makes this `mat[j]`; it is **not** a 2-D index.
* Passing `int mat[6][5]` where `int mat[5][6]` is expected — wrong, the column count must match.
* `double` must be printed with `%f` (or `%lf`), and read with `%lf` — using `%f` in `scanf` for a `double` is a bug.
* Forgetting the inner `{ }` braces when initialising rows → wrong layout (or an error).
* Omitting the column count in an initialiser: `int a[][] = {...}` is an **error**.
* `int *mat[5]` is an array of pointers; `int (*mat)[5]` is a pointer to an array. **Different types** — a guaranteed MCQ.

### Quick Recall
* `mat[i][j]` ≡ `*(*(mat+i)+j)`; rows are stored consecutively.
* In a function parameter you must fix the **column** count.
* Reading type expressions: start at the name, go inside-out with `()`/`[]` before `*`.

---

## 14. File handling

### Concept Summary
* A **file** is a **collection of bytes stored on secondary storage** such as hard disks. Anything addressable in the file system can be a file — including `/dev/null`, `/dev/urandom`, `/dev/audio`.
* **Three files are always connected to a program:**

| Stream | Contents | File descriptor | Functions that use it |
|---|---|---|---|
| `stdin` | standard input (usually the keyboard) | **0** | `scanf`, `getchar`, `gets` |
| `stdout` | standard output (usually the terminal) | **1** | `printf`, `putchar`, `puts` |
| `stderr` | standard error console | **2** | error messages |

### Shell redirection (NOT part of C)
| Command | Effect |
|---|---|
| `./a.out < inputfile` | read from `inputfile` instead of the keyboard |
| `./a.out > outfile` | write to `outfile` instead of the terminal |
| `./a.out 2> errfile` | send error messages to `errfile` instead of `stderr` |

* Redirection is provided by the **Linux shell**; it is **not** part of the C programming language. To handle **multiple** files inside a program, use C's file functions.

### The general scheme (3 steps)
```c
FILE *fp;                                  /* 1. OPEN — returns a file pointer */
fp = fopen("inputfile", "r");              /*    fp points to a struct holding the file's state */
if (fp == NULL) { /* open failed — exit */ }

int fscanf(FILE *fp, char *format, ...);   /* 2. READ / WRITE */
int fprintf(FILE *fp, char *format, ...);

int fclose(FILE *fp);                      /* 3. CLOSE — flushes and releases the file */
```
* **Compare with `scanf` and `printf`: the only difference is the extra first argument `fp`.**
* `fopen` returns **`NULL`** if it fails — always check.

### `fopen` modes (memorise the table)
| Mode | Meaning | File must exist? | Creates file? | Position of first write |
|---|---|---|---|---|
| `"r"` | read-only (any write fails) | **yes** | no | — |
| `"w"` | write | no | **yes** (else **overwrites/truncates**) | beginning |
| `"a"` | append | no | **yes** | end of current content |
| `"r+"` | read **and** write (update) | **yes** | no | beginning |
| `"w+"` | write/update | no | **yes** (empty file) | beginning |
| `"a+"` | append/update | no | **yes** | always at end (`fseek` affects the next **read** only) |

### Other file functions
| Function | Purpose |
|---|---|
| `int feof(FILE *fp)` | non-zero if the **EOF indicator** has been set (EOF has been encountered), else 0 |
| `int ferror(FILE *fp)` | non-zero if the **error indicator** is set (e.g. a write error) |
| `int fseek(FILE *fp, long offset, int origin)` | move the current position to `origin + offset` |
| `int ftell(FILE *fp)` | return the current value of the position indicator |
| `int fgetc(FILE *fp)` / `int getc(FILE *)` | read one character (**returns `int`** so `EOF` fits) |
| `int fputc(int c, FILE *fp)` / `putc` | write one character |

`fseek` origins: **`SEEK_SET`** = beginning of file, **`SEEK_CUR`** = current position, **`SEEK_END`** = end of file.

### Typical program shape
```c
#include <stdio.h>
int main() {
    FILE *fp;
    int c;
    fp = fopen("inputfile", "r");
    if (fp == NULL) return 1;                  /* always check! */
    while ((c = fgetc(fp)) != EOF)             /* c must be int, not char */
        putchar(c);
    fclose(fp);
    return 0;
}
```

### The "tail" exercise (design question)
* Goal: print the **last 10 lines** of a file.
* **Algorithm 1 (inefficient):** write a function that **reverses a file**, then print the first 10 lines of the reversed file and reverse each line again. *Problem: it reads the whole file.*
* **Better:** start at the **end of the file with `fseek`** and read backwards, collecting newline characters until 10 lines have been gathered.

### ⚠️ Traps
* **`fopen` failure not checked** → `NULL` pointer use → crash. A classic find-the-error.
* Reading with `"r"` a file that does not exist → `fopen` returns `NULL` (it does **not** create the file).
* Opening an existing file with `"w"` **destroys** its old contents.
* `"a"` writes at the **end** regardless of `fseek`; use `"r+"`/`"w+"` if you want to update in the middle.
* `fgetc`/`getchar` return **`int`** (to hold `EOF`); storing them in a `char` can break the `!= EOF` test.
* Forgetting `fclose` may lose buffered data.
* `feof()` is true only **after** a read has hit the end — the standard bug is to test it *before* the read and process one extra "phantom" record.

### Quick Recall
* `fopen` → `FILE *` (or `NULL`) · `fscanf`/`fprintf` take `fp` first · `fclose` releases the file.
* `stdin`=0, `stdout`=1, `stderr`=2; `<`, `>`, `2>` are **shell** features.
* `"r"` needs the file; `"w"` truncates; `"a"` appends.

---

## 15. Preprocessor, multiple source files & makefiles

### The C preprocessor
* The preprocessor implements a **macro language** that **transforms C programs BEFORE they are compiled**.
* **Lines that start with `#` are viewed as macros** and are handled by the preprocessor.
* Order of work: **source + headers → preprocessor → compiler → assembler → linker → executable**.
* The preprocessor also **removes comments**.

### `#include`
| Form | Searches |
|---|---|
| `#include <file>` | **system header files** — a standard list of system directories |
| `#include "file"` | **your own header files** — first the **directory containing the current file**, then the same directories as `<file>` |

* Including a header file produces **exactly the same result as copying that file into the source at the point of the `#include`**.
* Advantages: related declarations appear in **one place**; one file to change; all users see the change automatically.
* The argument behaves like a **string constant** — comments are not recognised and macros are not expanded inside it.
* `#include "..."` may also take a **full path**: `#include "/users/btech2115/banti/prog/list.h"`.

### `#define` — object-like macros
```c
#define PI      3.1416
#define BUF_SZ  1024
#define MAX     9999
```
* An **object-like macro** is an identifier that is **replaced by a code fragment** (it looks like a data object in the code that uses it).
* `char *str = calloc(BUF_SZ, sizeof(char));` — the compiler sees `calloc(1024, sizeof(char));`
* **By convention macro names are written in UPPER CASE** so that macros are easy to spot.
* Macros are **textual** substitutions — no type checking, no scope.
* **Sequential processing:** a macro definition takes effect **only at the place where it is written**.
```c
foo = X;          /* X is NOT yet defined here -> this is an error/unknown identifier */
#define X 4
bar = X;          /* becomes bar = 4; */
```
* `#define` lines take **no semicolon** (a semicolon would become part of the substitution).

### `#ifndef` / `#define` / `#endif` — include guards
**The problem:** file `p2.h` includes `p1.h`, and both include `list.h`. So `list.h` gets included **twice** → the structures get **re-defined** → error. This is a standard project-management problem.
**The solution:** give every header its own macro guard.
```c
#ifndef LIST_H          /* if LIST_H is NOT defined yet ... */
#define LIST_H          /* ... define it                           */
/* all the statements/directives in list.h */
#endif                  /* end of the guarded region               */
```
* If the macro is already defined, everything up to `#endif` is **skipped**. Adding a new file to the project then becomes safe.

### Separating `.h` and `.c` files
| File | Contains |
|---|---|
| `list.h` | **structure definitions, typedefs and function prototypes** (the *public interface*) |
| `list.c` | the **C code of the function definitions** |
| `prog.c` | the program that **uses** the functions — it only needs `#include "list.h"` |

* Programs that use the list functions need to know only the **declarations**, not the code: they are **"consumers"**.
* Functions written in `list.c` whose prototypes are **not** in `list.h` are **private** to `list.c`; files including `list.h` can never use them, or even know they exist. This is **information hiding / localisation**.
* **Advantages:** (1) saves repeated compilation — `list.c` need not be recompiled while `prog.c` changes; (2) information hiding; (3) modules that do not need to know the details of another module are not told them.

### Compiling and linking
```bash
gcc -c list.c                 # -> list.o   (object code; no main() required)
gcc -c prog.c                 # -> prog.o
gcc -o a.out prog.o list.o    # link -> executable a.out
gcc prog.c list.o             # alternative: compile prog.c and link with the already-built list.o
gcc -o prog prog.o list.o     # rename the executable to "prog"
```
* `-c` = compile to object code **only** (the linker is not run).
* Object files end in **`.o`** on Unix.
* Compiling large libraries takes time — **not** recompiling `list.c` every time speeds up the edit–compile–debug cycle.

### Makefiles (build automation)
```make
a.out: prog.o list.o
	gcc -o a.out prog.o list.o

prog.o: prog.c list.h
	gcc -c prog.c

list.o: list.c list.h
	gcc -c list.c

clean:
	rm -f *.o a.out
```
| Concept | Meaning |
|---|---|
| **target** | the file to be produced (left of `:`) |
| **dependencies** | files it needs (right of `:`) |
| **command** | the recipe, indented with a **TAB** |
| `make` | rebuilds only targets whose dependencies are **newer** |
| `make clean` | runs the `clean` target |

### ⚠️ Traps
* `#include` and `#define` take **no semicolon**.
* Macros are **textual** — `#define SQUARE(x) x*x` then `SQUARE(a+b)` expands to `a+b*a+b`, **wrong**; write `((x)*(x))`.
* A macro is **not a variable** — you cannot take its address or change it at run time.
* Without include guards, double inclusion causes **redefinition errors**.
* `gcc -c` produces `.o`; only the **linker** makes an executable.
* In a makefile, the command lines must start with a **TAB**, not spaces.

### Quick Recall
* `<>` = system headers, `""` = your headers.
* `#define NAME value` = textual substitution, sequential, no semicolon, UPPER CASE by convention.
* `#ifndef / #define / #endif` = include guard.
* `.h` = declarations, `.c` = definitions; `-c` = object code; linker = executable.

---

## 16. Linked lists (singly)

### Concept Summary
* A **linked list** is a chain of **nodes**, each holding a value and a **pointer to the next node**. The last node's `next` is **`NULL`**; the program keeps a **`head`** pointer to the first node.
* Unlike an array, the nodes are **not** consecutive in memory — the links provide the order.
* Node and list types:
```c
struct node {                    /* one node */
    int data;
    struct node *next;
};
typedef struct node * Nodeptr;   /* a convenient alias */
```
* A list is either **empty** (`head == NULL`) or one node whose `next` leads to the rest.

### Creating and traversing
```c
Nodeptr make_node(int val) {
    Nodeptr p = (Nodeptr) malloc(sizeof(struct node));   /* allocate on the HEAP */
    if (p != NULL) { p->data = val; p->next = NULL; }
    return p;
}
/* traversal — the standard loop */
for (p = head; p != NULL; p = p->next)
    printf("%d ", p->data);
```

### Core operations
```c
/* INSERT AT FRONT — easy, we already have the head pointer */
void insert_front(Nodeptr *head, int val) {
    Nodeptr n = make_node(val);
    n->next = *head;
    *head = n;                      /* head must be a POINTER TO POINTER to change it */
}

/* INSERT AFTER a given node — very quick, constant number of operations */
void insert_after(Nodeptr cur, int val) {
    Nodeptr n = make_node(val);
    n->next = cur->next;
    cur->next = n;                  /* order matters: set n->next BEFORE overwriting cur->next */
}

/* SEARCH — linear */
Nodeptr find(Nodeptr head, int v) {
    for (; head != NULL; head = head->next)
        if (head->data == v) return head;
    return NULL;
}

/* DELETE the node pointed to by pnode; ppnode is the PREVIOUS node (NULL if pnode is the head) */
struct node *delete(struct node *pnode, struct node *ppnode) {
    struct node *t;
    if (ppnode != NULL) ppnode->next = pnode->next;   /* unlink from the middle/end */
    else                t = pnode->next;              /* pnode is the HEAD */
    free(pnode);
    if (ppnode) return ppnode;
    else        return t;                             /* new head */
}
/* FREE the whole list: save next BEFORE freeing */
void free_list(Nodeptr head) {
    while (head != NULL) { Nodeptr next = head->next; free(head); head = next; }
}
```

### ⚠️ The four fatal list bugs
1. **Dereferencing `NULL`** at the end of the list (`while (p->next != NULL)` instead of `while (p != NULL)`).
2. **Losing the rest of the list** by writing `cur->next = n;` **before** copying the old `cur->next` into `n->next`.
3. **Forgetting the empty-list case** — inserting into an empty list, or deleting from it.
4. **Using `free(p)` and then reading `p->next`** (and forgetting that a function must take **`struct node **`** to be able to change `head`).

A deletion also requires a **pointer to the previous node**, which is exactly the limitation of a singly linked list.

### Pros and cons: linked list vs array
| Operation | Singly Linked List | Array |
|---|---|---|
| **Searching** | sequential (linear) search | sequential (linear) search |
| **Searching a sorted structure** | still sequential — **cannot take advantage** of sortedness | **binary search** possible (logarithmic) ✔ |
| **Insert a key after a given point** | **very quick** — a constant number of operations ✔ | shift all elements at/after the index one place right, then insert (**linear time**) |
| **Arbitrary access** `a[i]` | must walk the list (linear) | direct/random access ✔ |
| Memory | grows and shrinks on demand | fixed size decided at declaration |

### Operations available on a singly linked list (given a pointer to a node)
| Operation | Possible? |
|---|---|
| Find the **next** node | ✔ follow the `next` field |
| Find the **previous** node | ❌ **cannot** do it |
| Insert **before** a node | ❌ **cannot** do it |
| Insert **in front** of the list | ✔ easy — there is a pointer to the head |

> **Principal inadequacy of a singly linked list: navigation is ONE-WAY only** — from a node you can only move forward.

### ⚠️ Traps
* To change the `head` inside a function, the parameter must be **`struct node **head`** (pointer to pointer) — otherwise only the local copy changes.
* `while (p != NULL)` vs `while (p->next != NULL)` — using the second one means the last node is never processed and `p` may end up `NULL`.
* After deleting a node in the middle you must still keep the list reachable: adjust the previous node's `next` **before** freeing.
* `malloc` may return `NULL` — check it before assigning `p->data`.
* `typedef struct node * Nodeptr;` must come **before** you use `Nodeptr` in other declarations.

### Quick Recall
* List = nodes + `next` links + a `head`; the last `next` is **`NULL`**.
* Insert-after is O(1); find-previous and insert-before are impossible.
* A **doubly** linked list fixes exactly those two limitations.

---

## 16b. Doubly linked lists

### Concept Summary
* In a **doubly linked list** every node has **three fields**: the **data**, a pointer to the **previous** node, and a pointer to the **next** node.
* The list structure keeps **both** a `head` (first node) and a `last`/`tail` (last node), so appending is cheap.
```c
struct dllnode {
    int data;
    struct dllnode *next;
    struct dllnode *prev;
};
typedef struct dllnode * Ndptr;         /* pointer to a node */

struct dllist {
    Ndptr head;      /* first node */
    Ndptr last;      /* last node  */
};
typedef struct dllist * Dllist;         /* pointer to the list header */
```
* A **data structure** = the data (here, the list) + a **set of basic operations** supported on it.

### The operation set (from the slides — the API is a favourite MCQ source)
```c
Ndptr head(Dllist L);                                  /* returns head of L, L non-null  */
Ndptr tail(Dllist L);                                  /* returns pointer to last node    */
void  insert_before_node(Dllist L, Ndptr pcurr, Ndptr pnew);
void  insert_after_node (Dllist L, Ndptr pcurr, Ndptr pnew);
Dllist append(Dllist L, Ndptr p);                      /* add at the TAIL                */
int   isEmpty(Dllist L);                               /* 1 if empty, else 0             */
Dllist simple_concat(Dllist L1, Dllist L2);            /* join by re-linking (fast)      */
Dllist deep_concat  (Dllist L1, Dllist L2);            /* join by COPYING nodes          */
Dllist copy_list(Dllist L);                            /* duplicate the whole list       */
void  delete_node(Dllist L, Ndptr p);                  /* unlink AND free                */
void  extract_node(Dllist L, Ndptr p);                 /* unlink WITHOUT freeing         */
void  delete_list_hdr(Dllist L);                        /* free the list header           */
```

### Key implementations
```c
Dllist make_list(Ndptr pnew) {                       /* create an empty/one-node list */
    Dllist L = calloc(1, sizeof(*L));
    L->head = L->last = pnew;
    if (pnew) pnew->prev = pnew->next = NULL;
    return L;
}
int isEmpty(Dllist L) { return (!L || !L->head) ? 1 : 0; }

Dllist insert_after_node(Dllist L, Ndptr pcurr, Ndptr pnew) {
    if (!L) return make_list(pnew);
    if (L->head == NULL) { L->head = L->last = pnew; return L; }   /* empty list */
    if (!pcurr) return L;                                          /* error      */
    pnew->next = pcurr->next;
    pnew->prev = pcurr;
    if (pcurr->next) pcurr->next->prev = pnew;   /* fix the successor's back pointer */
    else             L->last = pnew;             /* pcurr was the tail              */
    pcurr->next = pnew;
    return L;
}

Dllist insert_before_node(Dllist L, Ndptr pcurr, Ndptr pnew) {
    if (!L) return make_list(pnew);
    if (L->head == NULL) { L->head = L->last = pnew; return L; }
    if (!pcurr) return L;                        /* error */
    pnew->next = pcurr;
    pnew->prev = pcurr->prev;
    if (pcurr->prev) pcurr->prev->next = pnew;
    else             L->head = pnew;             /* pcurr was the head */
    return L;
}

Dllist simple_concat(Dllist L1, Dllist L2) {     /* re-links; NO copying */
    if (isEmpty(L1)) return L2;
    if (isEmpty(L2)) return L1;
    L2->head->prev = L1->last;
    L1->last->next = L2->head;    /* use the OLD last node before updating it */
    L1->last       = L2->last;
    return L1;
}

void delete_node(Dllist L, Ndptr p) {            /* head / tail / middle in two steps */
    if (isEmpty(L) || !p) return;
    if (p->prev) p->prev->next = p->next;    /* unlink forward  */
    else         L->head = p->next;          /* p was the head  */
    if (p->next) p->next->prev = p->prev;    /* unlink backward */
    else         L->last = p->prev;          /* p was the tail  */
    free(p);                                 /* a one-node list ends with head = last = NULL */
}
void extract_node(Dllist L, Ndptr p) { /* same code as delete_node, except for free(p) */ }
```

### `simple_concat` vs `deep_concat`
| | `simple_concat` | `deep_concat` |
|---|---|---|
| Effect | **splices** the two lists by re-linking (`L1->last->next = L2->head`) | makes **copies** of both lists and joins the copies |
| Speed | very fast (constant work) | linear in the number of nodes |
| Side effect | **shares** the nodes, so changing one list changes the other | lists remain **independent** |
| Implementation | re-link pointers | `copy_list(L1)` + `copy_list(L2)` + `simple_concat` |

### Doubly vs singly linked list
| Operation | Singly | Doubly |
|---|---|---|
| Find next node | ✔ | ✔ |
| **Find previous node** | ❌ | ✔ (the whole point) |
| **Insert before a node** | ❌ | ✔ |
| Delete a node given only that node | ❌ (need the previous node) | ✔ |
| Memory per node | 1 pointer | 2 pointers |
| Complexity of the code | simpler | more pointer fixes at each step (`prev` AND `next` must be updated) |

### ⚠️ Traps
* In a doubly linked list you must update **both** `prev` and `next` at every step — forgetting `pcurr->next->prev = pnew;` silently breaks backward traversal.
* Special cases: **empty list**, **inserting before the head**, **deleting the head**, **deleting the tail**, **single-node list** — the API explicitly says the boundary cases must be completely defined.
* `delete_node` returns `void` and frees the node; `extract_node` just unlinks.
* Mixing up `L->last` and `L->tail`; the slides' struct field is named **`last`** while the accessor function is named **`tail`**.
* Returning after `free(p)` and touching `p` again → use-after-free.

### Quick Recall
* Doubly linked list node = `data` + `prev` + `next`; the list header = `head` + `last`.
* Doubly linked lists make **find-previous** and **insert-before** possible.
* `simple_concat` shares nodes; `deep_concat` copies them.
* Allocation/`free` should happen in **one or two well-defined library functions** (`make_empty_list`, `make_node`), and the library should provide the routines to free the memory it allocated.

---

## 17. Practice MCQs — Set 1 (with answers and reasoning)

> Try to answer before looking at the answer line. These are exactly the style NPTEL uses.

**Q1.** Which of the following is the correct way to read an integer into `x`?
(a) `scanf("%d", x);`  (b) `scanf("%d", &x);`  (c) `scanf("%d", *x);`  (d) `scanf(&x, "%d");`
**Ans: (b).** `scanf` needs the **address** of the variable.

**Q2.** What is printed?
```c
int a = 7, b = 2;
printf("%d", a/b);
```
(a) 3.5  (b) 4  (c) 3  (d) 1
**Ans: (c) 3.** Integer divided by integer is integer; the fraction is **discarded**, not rounded.

**Q3.** What is printed?
```c
printf("%d", 10 - 5 - 15);
```
(a) 0  (b) -10  (c) 20  (d) -20
**Ans: (b) -10.** `-` is left-associative: `((10-5)-15)`.

**Q4.** What is the value of `a`?
```c
int a;  a = 10 + 5 * 4 % 2;
```
(a) 10  (b) 20  (c) 0  (d) 30
**Ans: (a) 10.** `5*4 = 20`, `20 % 2 = 0`, `10 + 0 = 10`.

**Q5.** `if (x = 0)` — how many times will the body execute for any value of `x`?
(a) once  (b) never  (c) depends on `x`  (d) compile error
**Ans: (b) never.** It is an **assignment**, `x` becomes 0 and the value of the expression is 0 = FALSE.

**Q6.** Which statement about `do-while` is TRUE?
(a) the body may execute zero times  (b) the body executes at least once
(c) it has no condition  (d) `while(expr)` needs no semicolon
**Ans: (b).** The test comes **after** the body. (And the `;` after `while(expr)` **is** required.)

**Q7.** How many times does this loop execute?
```c
int i;  for (i = 0; i < 5; i = i + 2) printf("%d ", i);
```
(a) 5  (b) 3  (c) 2  (d) infinite
**Ans: (b) 3.** `i = 0, 2, 4` — it prints `0 2 4`.

**Q8.** What does `continue` do?
(a) exits the loop  (b) exits the program  (c) skips the rest of the current iteration
(d) restarts the whole program
**Ans: (c).**

**Q9.** What does `break` inside a `switch` do?
(a) exits the program  (b) exits the innermost loop and the switch
(c) exits the innermost loop or switch  (d) nothing
**Ans: (c).**

**Q10.** A `switch` expression may be of which type?
(a) `float`  (b) `double`  (c) `int` or `char`  (d) any type
**Ans: (c).** `float`/`double`/strings are **not** allowed in `switch`.

**Q11.** What is printed?
```c
int i = 5;  printf("%d %d", i++, ++i);
```
(a) 5 7  (b) 6 7  (c) undefined behaviour  (d) 5 6
**Ans: (c).** The same variable is modified twice between sequence points — **undefined behaviour**.

**Q12.** `int i = 5; printf("%d", i++); printf("%d", i);` prints
(a) 5 5  (b) 5 6  (c) 6 6  (d) 6 5
**Ans: (b) 5 6.** Postfix uses the old value, then increments.

**Q13.** In `a && b`, if `a` is 0 then
(a) `b` is always evaluated  (b) `b` is never evaluated  (c) both are evaluated  (d) error
**Ans: (b).** `&&` **short-circuits**.

**Q14.** What is the value of `5 & 3`?
(a) 1  (b) 7  (c) 8  (d) 0
**Ans: (a) 1.** Bitwise AND of `101` and `011` is `001`.

**Q15.** Which is TRUE about C function arguments?
(a) arrays are passed by value in the usual sense  (b) all arguments are passed by value
(c) all arguments are passed by reference  (d) only pointers are passed by value
**Ans: (b).** C is **call by value**; you emulate call-by-reference using pointers.

**Q16.** For the function below, what does the caller's `a` contain afterwards?
```c
void swap(int a, int b) { int t = a; a = b; b = t; }
int main() { int a = 1, b = 2; swap(a, b); }
```
(a) 2  (b) 1  (c) undefined  (d) 0
**Ans: (b) 1.** The changes are made to **copies** and are lost.

**Q17.** Which statement about `return;` (no expression) in a function declared to return `float` is TRUE?
(a) it returns 0  (b) it returns the last computed value  (c) the returned value is unpredictable
(d) compile error
**Ans: (c).** The return value is **garbage**.

**Q18.** `int num[10];` — what is `sizeof(num)` on a machine with 4-byte `int`s?
(a) 10  (b) 4  (c) 40  (d) 8
**Ans: (c) 40.** `sizeof` of an array = total bytes = `10 * sizeof(int)`.

**Q19.** Inside a function declared as `void f(int a[])`, `sizeof(a)` gives
(a) the array size in bytes  (b) the number of elements  (c) the size of a pointer  (d) a compile error
**Ans: (c).** The array **decays** to a pointer when passed.

**Q20.** `int a[10];` — which index is the last valid one?
(a) 10  (b) 9  (c) 11  (d) 1
**Ans: (b) 9.** Indices run `0 … n-1`.

**Q21.** `a[i]` is exactly equivalent to
(a) `*(a+i)`  (b) `*a + i`  (c) `&a + i`  (d) `a + i`
**Ans: (a) `*(a+i)`.**

**Q22.** Declaring `int *p;`, what does `p + 1` advance by?
(a) 1 byte  (b) 4 bytes  (c) 8 bytes  (d) 1 element
**Ans: (b) 4 bytes** (and 1 element) — `p + i` is `p + i*sizeof(type)` on a 4-byte int machine.

**Q23.** `int num[] = {5, 10, 15, 20};` — what is `num[3]`?
(a) 15  (b) 20  (c) 0  (d) garbage
**Ans: (b) 20.**

**Q24.** `int num[10] = {1, 2, 3};` — what is `num[7]`?
(a) garbage  (b) 0  (c) 3  (d) compile error
**Ans: (b) 0.** Remaining elements are initialised to 0.

**Q25.** `int num[6] = {1,2,3,4,5,6,7};` — this is
(a) legal, size becomes 7  (b) a compile error  (c) legal, `num[6]` is ignored  (d) undefined
**Ans: (b).** The number of initialisers must be ≤ the declared size.

**Q26.** A C string is terminated by
(a) `'\n'`  (b) `EOF`  (c) `'\0'`  (d) `" "`
**Ans: (c) `'\0'`.**

**Q27.** `char s[] = "hello";` — what does `strlen(s)` return?
(a) 6  (b) 5  (c) 4  (d) 0
**Ans: (b) 5.** `strlen` does **not** count the `'\0'`; `sizeof(s)` would be **6**.

**Q28.** What is printed?
```c
char str[] = "I am GR8DON";
str[4] = '\0';
printf("%s", str);
```
(a) I am GR8DON  (b) I am  (c) I amGR8DON  (d) nothing
**Ans: (b) `I am`.** `%s` stops at the first `'\0'`.

**Q29.** To convert a `float` to an `int`, the C cast is
(a) `int(x)`  (b) `(int) x`  (c) `int x`  (d) `cast<int>(x)`
**Ans: (b).** Casting truncates rather than rounds.

**Q30.** `float x = 5.674157;` — `printf("%d", (int)x);` prints
(a) 6  (b) 5.67  (c) 5  (d) undefined
**Ans: (c) 5.** Truncation toward zero.

---

## 17b. Practice MCQs — Set 2 (answers and reasoning)

**Q31.** `int y = 10000009; printf("%f", (float)y); printf(" %d", y);` prints
(a) `10000009.000000 10000009`  (b) `10000008.000000 10000009`
(c) `10000009.000000 10000008`  (d) `0.000000 10000009`
**Ans: (b).** `float` has only ~7 significant digits — information is **lost** in the conversion, but `y` itself is unchanged.

**Q32.** Converting a `float` value that is too large for an `int` (e.g. `1.0E50`) is
(a) rounded  (b) truncated  (c) undefined  (d) a compile error
**Ans: (c) undefined.** "Careful when converting from a larger type to a smaller type. Undefined."

**Q33.** A pointer stores
(a) the value of a variable  (b) the address of a variable  (c) the name of a variable  (d) a copy of a variable
**Ans: (b).**

**Q34.** `&` is the ______ operator and `*` (on a pointer) is the ______ operator.
(a) dereference, address-of  (b) address-of, dereference  (c) multiply, address-of  (d) bitwise, logical
**Ans: (b).**

**Q35.** Comparing two pointers with `<` is well-defined only if
(a) they are of type `int *`  (b) they point into the **same array**
(c) they are both `NULL`  (d) they are `void *`
**Ans: (b).** Otherwise it is undefined behaviour.

**Q36.** `scanf("%d", ptr);` where `ptr` is an `int *` pointing to `num[1]`:
(a) is a compile error  (b) reads an integer into `num[1]`  (c) reads into `ptr`  (d) undefined
**Ans: (b).** `scanf` reads **into the box pointed to** by the argument.

**Q37.** Which correctly allocates 10 integers on the heap?
(a) `int *p = malloc(10);`  (b) `int *p = (int *)malloc(10*sizeof(int));`
(c) `int *p = (int)malloc(10);`  (d) `malloc(int, 10);`
**Ans: (b).**

**Q38.** Returning the address of a local variable from a function gives
(a) a copy  (b) a dangling pointer  (c) a NULL pointer  (d) a void pointer
**Ans: (b) a dangling pointer** — the local's memory is erased when the function returns.

**Q39.** Which header declares `malloc` and `free`?
(a) `stdio.h`  (b) `stdlib.h`  (c) `string.h`  (d) `math.h`
**Ans: (b) `stdlib.h`.**

**Q40.** Forgetting to `free` memory that was allocated is called
(a) a dangling pointer  (b) a memory leak  (c) a buffer overflow  (d) garbage collection
**Ans: (b) a memory leak.**

**Q41.** Calling `free` twice on the same non-NULL pointer is
(a) safe  (b) a runtime error  (c) a memory leak  (d) ignored by the compiler
**Ans: (b) a runtime error.** (`free(NULL)` *is* safe.)

**Q42.** A recursive function must have
(a) a loop  (b) a base case  (c) a pointer  (d) a global variable
**Ans: (b) a base case.** Without it, infinite recursion → stack overflow.

**Q43.** Naïve recursive `fib(n) = fib(n-1) + fib(n-2)` is
(a) linear time  (b) logarithmic time  (c) exponential (very inefficient)  (d) constant time
**Ans: (c).** The number of calls grows like `Fₙ`; the same subproblems are recomputed.

**Q44.** The stack depth of the two-way recursive `max_arr` (halving the array) is about
(a) n  (b) n/2  (c) 1 + log₂ n  (d) n²
**Ans: (c) ~1 + log₂ n.** The linear version's depth is n.

**Q45.** What is the depth of recursion?
(a) the number of recursive calls ever made  (b) the maximum number of **pending** calls
(c) the number of parameters  (d) the value of the base case
**Ans: (b).**

**Q46.** In which module is `sqrt` declared, and how do you link it?
(a) `stdio.h`, no flag  (b) `math.h`, with `-lm`  (c) `stdlib.h`, with `-lm`  (d) `math.h`, no flag
**Ans: (b) `math.h` + `gcc file.c -lm`.**

**Q47.** The correct declaration of a function taking a `struct point` by value and returning one is
(a) `point f(point p)`  (b) `struct point f(struct point p)`  (c) `f(struct point)`  (d) `void f(struct point p)`
**Ans: (b).** Unless you `typedef` it, the type name must be written **`struct point`**.

**Q48.** If `p` is a `struct point *`, then `p->x` is the same as
(a) `*p.x`  (b) `(*p).x`  (c) `&p.x`  (d) `p.x`
**Ans: (b) `(*p).x`.**

**Q49.** `pts[i].x` is read as
(a) `pts[i.x]`  (b) `(pts[i]).x`  (c) `pts[(i.x)]`  (d) error
**Ans: (b).** `.` and `[]` have equal precedence with left→right associativity.

**Q50.** `int (*mat)[5]` means
(a) an array of 5 pointers to int  (b) a pointer to an array of 5 ints
(c) a pointer to a pointer to int  (d) an array of 5 ints
**Ans: (b).** (`int *mat[5]` is the array of 5 pointers.)

---

## 17c. Practice MCQs — Set 3 (answers and reasoning)

**Q51.** For a 2-D array `double mat[5][6]`, which index expression is correct?
(a) `mat[3][4]`  (b) `mat[3,4]`  (c) `mat(3)(4)`  (d) `mat{3}{4}`
**Ans: (a).** `mat[3,4]` uses the **comma operator** and means `mat[4]`.

**Q52.** When a 2-D array is passed to a function, which dimension(s) must be specified?
(a) rows  (b) columns  (c) both  (d) neither
**Ans: (b) columns.**

**Q53.** `mat[i][j]` for `int (*mat)[5]` is equivalent to
(a) `*(mat+i+j)`  (b) `*(*(mat+i)+j)`  (c) `**(mat+i+j)`  (d) `*(mat+i)[j]`
**Ans: (b).**

**Q54.** `int a[][3] = {{1},{2,3},{3,4,5}};` — what is `a[0][1]`?
(a) 2  (b) 0  (c) 3  (d) garbage
**Ans: (b) 0.** Missing row values are set to 0.

**Q55.** `char *mnth[] = {"Jan","Feb", ...};` — what is the type of `mnth`?
(a) `char`  (b) `char *`  (c) `char **`  (d) `char [12]`
**Ans: (c) `char **`.** (`mnth[0]` is `char *`, `mnth[0][0]` is `char`.)

**Q56.** Which `fopen` mode requires an existing file?
(a) `"r"`  (b) `"w"`  (c) `"a"`  (d) `"w+"`
**Ans: (a) `"r"`.** (`"w"` and `"a"` create the file if it is absent.)

**Q57.** Opening an existing file in `"w"` mode
(a) appends  (b) fails  (c) discards the old contents  (d) reads first
**Ans: (c).**

**Q58.** `fopen` returns ______ on failure.
(a) `0`  (b) `-1`  (c) `NULL`  (d) `EOF`
**Ans: (c) `NULL`.**

**Q59.** The correct signature of `fopen` is
(a) `int fopen(char *name, char *mode)`  (b) `FILE *fopen(char *name, char *mode)`
(c) `FILE fopen(char *mode)`  (d) `void fopen(FILE *fp, char *name)`
**Ans: (b).**

**Q60.** `feof(fp)` returns
(a) `EOF`  (b) non-zero if the EOF indicator is set  (c) the file size  (d) the current position
**Ans: (b).** It becomes true only **after** the attempt to read past the end.

**Q61.** `fseek(fp, 0, SEEK_END)` moves the position to
(a) the beginning  (b) the current position  (c) the **end of the file**  (d) 0 bytes
**Ans: (c).**

**Q62.** `ftell(fp)` returns
(a) the file size always  (b) the current value of the position indicator
(c) the number of lines  (d) `EOF`
**Ans: (b).**

**Q63.** Which argument does `fprintf` have that `printf` does not?
(a) a `FILE *` first argument  (b) a length argument  (c) a mode string  (d) none
**Ans: (a).**

**Q64.** Which file descriptor corresponds to `stdout`?
(a) 0  (b) 1  (c) 2  (d) 3
**Ans: (b) 1.** (`stdin` = 0, `stderr` = 2.)

**Q65.** `./a.out < inputfile` is implemented by
(a) the C program  (b) the compiler  (c) the shell  (d) the linker
**Ans: (c) the shell.** Redirection is **not** part of the C language.

**Q66.** `#include "list.h"` searches
(a) only system directories  (b) the directory of the current file first, then system directories
(c) only the current file  (d) nowhere
**Ans: (b).**

**Q67.** A header guard is written as
(a) `#ifdef / #endif`  (b) `#ifndef / #define / #endif`  (c) `#define / #undef`  (d) `#pragma once` only
**Ans: (b).** It prevents a header being processed twice.

**Q68.** `#define BUF_SZ 1024` is best described as
(a) a variable  (b) an object-like macro replaced textually by the preprocessor
(c) a function  (d) a constant that can be assigned to
**Ans: (b).**

**Q69.** Which gcc command produces **object code only**?
(a) `gcc prog.c`  (b) `gcc -c prog.c`  (c) `gcc -o prog prog.c`  (d) `gcc -lm prog.c`
**Ans: (b) `gcc -c`.**

**Q70.** In the compilation pipeline, which stage runs **first**?
(a) compiler  (b) linker  (c) preprocessor  (d) assembler
**Ans: (c) preprocessor.**

**Q71.** For a singly linked list, which operation is **impossible** given only a pointer to an arbitrary node?
(a) finding the next node  (b) finding the previous node  (c) freeing that node  (d) printing its data
**Ans: (b).** Navigation is **one-way only**.

**Q72.** Inserting a key immediately after a given node in a linked list takes
(a) linear time  (b) constant time  (c) logarithmic time  (d) quadratic time
**Ans: (b).** Compare with arrays, which need shifting (linear).

**Q73.** On a **sorted** array we can use ______, which is impossible on a linked list.
(a) linear search  (b) binary search  (c) hashing  (d) sequential scan
**Ans: (b) binary search** (logarithmic).

**Q74.** To allow a function to change the `head` of a linked list, its parameter should be
(a) `struct node *head`  (b) `struct node **head`  (c) `struct node head`  (d) `void *head`
**Ans: (b) a pointer to a pointer.**

**Q75.** A doubly linked list node contains
(a) `data, next`  (b) `data, next, prev`  (c) `data, key`  (d) `head, tail`
**Ans: (b).**

**Q76.** `simple_concat(L1, L2)` differs from `deep_concat(L1, L2)` in that it
(a) copies the nodes  (b) re-links the existing nodes (no copying)  (c) frees the lists  (d) sorts them
**Ans: (b).**

**Q77.** `extract_node` differs from `delete_node` in that it
(a) does not unlink the node  (b) does not `free` the node  (c) does not exist  (d) frees the whole list
**Ans: (b).**

**Q78.** The value of `strlen("hello")` and `sizeof("hello")` are respectively
(a) 5 and 5  (b) 5 and 6  (c) 6 and 5  (d) 6 and 6
**Ans: (b) 5 and 6.** `strlen` excludes the `'\0'`; `sizeof` includes it.

**Q79.** Which statement about `printf("%s", str)` is TRUE?
(a) it prints the whole array regardless of `'\0'`  (b) it stops at the first `'\0'`
(c) it prints only the first character  (d) it prints the length of `str`
**Ans: (b).**

**Q80.** In `for (i = 0; i < n; i = i + 1)`, how many times is the loop body executed?
(a) n-1  (b) n  (c) n+1  (d) depends on the body
**Ans: (b) n**, for `i = 0,1,…,n-1`.

---

## 18. Fill-in-the-blank bank (with answers)

> Cover the Answer column, fill it in, then check. Every item comes from the lecture slides.

### Headers, keywords and syntax
| # | Fill in the blank | Answer |
|---|---|---|
| 1 | To use `printf` and `scanf`, include the header ______. | `<stdio.h>` |
| 2 | To use `malloc`, `calloc` and `free`, include ______. | `<stdlib.h>` |
| 3 | To use `strlen`, `strcpy`, `strcmp`, include ______. | `<string.h>` |
| 4 | To use `sqrt`, include ______ and link with ______. | `<math.h>`, `-lm` |
| 5 | Every C statement must end with a ______. | semicolon `;` |
| 6 | A group of statements enclosed in `{ }` is called a ______ statement or a ______. | compound, block |
| 7 | C is ______-sensitive, so `Main` and `main` are different. | case |
| 8 | Execution of a C program always begins at the function ______. | `main` |
| 9 | The value `main` returns to mean "success" is ______. | `0` |
| 10 | Compiling with `gcc` without `-o` produces an executable named ______. | `a.out` |

### Types, input/output and conversion
| # | Fill in the blank | Answer |
|---|---|---|
| 11 | The format specifier for an `int` is ______. | `%d` |
| 12 | The format specifier for `float` in `scanf` is ______; for `double` it is ______. | `%f`, `%lf` |
| 13 | The format specifier to print a character is ______; for a string it is ______. | `%c`, `%s` |
| 14 | `scanf` needs the ______ of the variable, written with the ______ operator. | address, `&` |
| 15 | The ASCII code of `'A'` is ______ and of `'a'` is ______. | 65, 97 |
| 16 | ASCII code `'0'` is ______; the NULL character `'\0'` is ______. | 48, 0 |
| 17 | `sizeof(char)` = ______, `sizeof(int)` = ______ (typical). | 1, 4 |
| 18 | Casting a `float` to an `int` ______ the fractional part. | truncates (discards) |
| 19 | Converting a value of a larger type into a smaller type is called ______. | narrowing — the value is truncated; undefined only if it does not fit |
| 20 | `printf` returns the number of ______; `scanf` returns the number of ______. | characters printed, items successfully read |
| 21 | The type of a character constant such as `'A'` is ______. | `char` (an integer type) |
| 22 | `%d` and `%f` in `scanf` skip leading ______; `%c` does ______. | whitespace, not |

### Operators
| # | Fill in the blank | Answer |
|---|---|---|
| 23 | `8 % 3` evaluates to ______. | 2 |
| 24 | `7 / 2` evaluates to ______ and `7 % 2` evaluates to ______. | 3, 1 |
| 25 | The operator `%` cannot be used with ______ operands. | floating point (`float`/`double`) |
| 26 | The assignment operator `=` is ______-associative. | right |
| 27 | Binary `+`, `-`, `*`, `/`, `%` are ______-associative. | left |
| 28 | `10 - 5 - 15` evaluates to ______. | -10 |
| 29 | `i++` uses the ______ value then increments; `++i` increments then uses the ______ value. | old, new |
| 30 | The operators `&&` and `||` perform ______ evaluation. | short-circuit |
| 31 | `&&`, `||`, `!` are ______ operators; `&`, `|`, `^`, `~` are ______ operators. | logical, bitwise |
| 32 | `sizeof` is an ______, not a function. | operator |
| 33 | The value of `!0` is ______; the value of `!5` is ______. | 1, 0 |
| 34 | Any non-zero value is treated as ______; zero is treated as ______. | TRUE, FALSE |
| 35 | A relational expression has type ______ with values ______ or ______. | `int`, 0, 1 |
| 36 | `a = 10 + 5 * 4 % 2` assigns ______ to `a`. | 10 |
| 37 | In `a = b = c = 0;` the assignments happen from ______ to ______. | right, left |
| 38 | Modifying the same variable twice between sequence points leads to ______. | undefined behaviour |

### Control flow
| # | Fill in the blank | Answer |
|---|---|---|
| 39 | `if` executes its body when the expression is ______. | non-zero |
| 40 | In `if-else`, when the expression is FALSE the ______ branch executes. | `else` |
| 41 | The branch of a `switch` that runs when no case matches is labelled ______. | `default` |
| 42 | Without a ______, control "falls through" to the next `case`. | `break` |
| 43 | The `switch` expression must be of ______ type. | integer |
| 44 | In a `switch`, case labels must be ______ and ______. | constant expressions, unique |
| 45 | `break` exits the ______ enclosing loop or switch. | nearest (innermost) |
| 46 | `continue` skips the rest of the current ______. | iteration |
| 47 | `if (x = 0)` is an ______, not a comparison, and is always ______. | assignment, false |
| 48 | In `if (a) if (b) s1; else s2;` the `else` belongs to the ______ `if`. | inner/nearest (`if (b)`) |

### Loops
| # | Fill in the blank | Answer |
|---|---|---|
| 49 | In a `while` loop the condition is tested ______ the body executes. | before |
| 50 | The loop whose body executes at least once is ______. | `do-while` |
| 51 | `do { ... } while (expr)` requires a ______ after `while (expr)`. | semicolon |
| 52 | `while` and `do-while` are equally ______. | expressive |
| 53 | A property that holds at the start of every iteration is a loop ______. | invariant |
| 54 | `for (i=0; i<n; i=i+1)` executes its body ______ times. | n |
| 55 | A doubly nested loop of n iterations each executes the innermost body ______ times. | n² |
| 56 | Bubble sort performs about ______ comparisons. | n(n-1)/2 |
| 57 | Binary search takes about ______ steps. | log₂ n |
| 58 | A right-angled triangle pattern of n rows prints ______ items. | n(n+1)/2 |

---

## 18b. Fill-in-the-blank bank — continued

### Functions
| # | Fill in the blank | Answer |
|---|---|---|
| 59 | Values supplied at the call are the ______ parameters; those in the definition are the ______ parameters. | actual, formal |
| 60 | In C, arguments are always passed by ______. | value |
| 61 | The ______ statement is the only mechanism for returning a value. | `return` |
| 62 | Executing `return` in `main` causes the program to ______. | terminate |
| 63 | Parameter values are copied in ______. | sequence (in order) |
| 64 | Memory for formal parameters and locals is allocated on the ______ and freed when the function ______. | stack, returns |
| 65 | To modify a caller's variable, a function must receive a ______. | pointer (address) |
| 66 | The order in which function arguments are evaluated is ______ in C. | unspecified (compiler dependent) |
| 67 | A `return;` with no expression makes the return value ______. | unpredictable / garbage |
| 68 | A function that calls itself is ______. | recursive |
| 69 | A function that returns nothing has return type ______. | `void` |
| 70 | The maximum number of pending calls is the ______ of recursion. | depth |
| 71 | Local variables and formal parameters are visible only ______ the function. | within/inside |
| 72 | A function can be used before its definition only if a ______ is given above. | prototype (forward declaration) |
| 73 | Writing a function that swaps two integers requires parameters of type ______. | `int *` |
| 74 | `void swap(int a, int b)` fails to swap because the changes are made to ______. | copies of the arguments |

### Arrays, strings and pointers
| # | Fill in the blank | Answer |
|---|---|---|
| 75 | Array indices in C start at ______. | 0 |
| 76 | The last element of `int a[10]` is `a[______]`. | 9 |
| 77 | In `int a[] = {1,2,3};` the array size is ______. | 3 |
| 78 | In `int a[10] = {1,2,3};` the remaining elements are set to ______. | 0 |
| 79 | The array name holds the address of the ______ element. | first (base) |
| 80 | `a[i]` is equivalent to ______. | `*(a+i)` |
| 81 | A C string is terminated by ______. | `'\0'` |
| 82 | `strlen(s)` counts the characters ______ the `'\0'`. | before (excluding) |
| 83 | `sizeof("hello")` is ______ while `strlen("hello")` is ______. | 6, 5 |
| 84 | The operator `&` gives the ______; `*` on a pointer gives the ______. | address, value it points to |
| 85 | `ptr + i` is the byte address `ptr + i * ______`. | `sizeof(type)` |
| 86 | `sizeof(array)` returns the size in ______. | bytes |
| 87 | An array passed to a function is said to ______ to a pointer. | decay |
| 88 | A pointer to memory that has been released is a ______ pointer. | dangling |
| 89 | Memory allocated with `malloc` lives on the ______. | heap |
| 90 | Freeing the same memory twice causes a ______ error. | runtime |
| 91 | Not freeing allocated memory is called a memory ______. | leak |
| 92 | A size-`n` string needs `malloc(______)` bytes. | `n+1` |
| 93 | `mat[i][j]` for a 2-D array equals ______. | `*(*(mat+i)+j)` |
| 94 | In `int (*mat)[5]`, `mat` is a pointer to ______. | an array of 5 ints |
| 95 | In `int *mat[5]`, `mat` is an array of ______. | 5 pointers to int |
| 96 | In `int **mat`, `mat` is a ______. | pointer to a pointer to int |
| 97 | When passing a 2-D array to a function, the number of ______ must be specified. | columns |
| 98 | `int a[][3] = {{1},{2,3}};` leaves the missing values as ______. | 0 |

---

## 18c. Fill-in-the-blank bank — structures, files, preprocessor, lists

| # | Fill in the blank | Answer |
|---|---|---|
| 99 | The members of a structure are called its ______. | fields |
| 100 | Fields of a structure **variable** are accessed with the ______ operator. | `.` (dot) |
| 101 | Fields of a structure **pointer** are accessed with the ______ operator. | `->` |
| 102 | `p->x` is equivalent to ______. | `(*p).x` |
| 103 | In `struct point { int x; int y; };` the `;` after `}` is ______. | mandatory (required) |
| 104 | Structure variables may be copied with ______, but two structures may not be compared with ______. | `=`, `==` |
| 105 | The three standard streams are ______, ______, ______ with descriptors ______, ______, ______. | stdin, stdout, stderr; 0, 1, 2 |
| 106 | `fopen` returns a value of type ______, or ______ on failure. | `FILE *`, `NULL` |
| 107 | The file mode that requires the file to exist and forbids writing is ______. | `"r"` |
| 108 | The file mode that creates a new file or truncates an existing one is ______. | `"w"` |
| 109 | The file mode that writes at the end of the existing content is ______. | `"a"` |
| 110 | `fseek` origins are ______, ______ and ______. | `SEEK_SET`, `SEEK_CUR`, `SEEK_END` |
| 111 | The function that reports end-of-file is ______; the one that reports an error is ______. | `feof`, `ferror` |
| 112 | On the terminal, end-of-file is typed as ______ (EOT, ASCII `\x4`). | `Ctrl-D` |
| 113 | `fgetc` returns type ______ so that it can hold `EOF`. | `int` |
| 114 | The directive used for your own header files is ______. | `#include "file"` |
| 115 | The three directives that form an include guard are ______, ______ and ______. | `#ifndef`, `#define`, `#endif` |
| 116 | The gcc option that compiles to object code only is ______. | `-c` |
| 117 | The program that combines object files into an executable is the ______. | linker |
| 118 | The preprocessor runs ______ the compiler. | before |
| 119 | `#define BUF_SZ 1024` creates an ______-like macro. | object |
| 120 | Macro substitution is purely ______ (no type checking). | textual |
| 121 | In a singly linked list each node holds the data and a pointer to the ______ node. | next |
| 122 | The link of the last node of a linked list is ______. | `NULL` |
| 123 | A linked list keeping `head` and `last` with `prev` and `next` in each node is a ______ linked list. | doubly |
| 124 | `simple_concat` joins lists by ______; `deep_concat` joins them by ______. | re-linking, copying |
| 125 | The principal inadequacy of a singly linked list is that navigation is ______ only. | one-way |
| 126 | The shell feature that sends a file's contents to a program's `stdin` is ______. | input redirection `<` |
| 127 | `struct node *next` inside `struct node` is called a ______ reference. | self (recursive) |
| 128 | `typedef struct node * Nodeptr;` creates an ______ for the type. | alias |

---

## 19. Find-the-error bank

> Each snippet contains exactly one error. Identify it, then read the fix. **Check in this order: `;` → `&` in `scanf` → `=` vs `==` → format specifier → missing braces → bounds → pointer validity.**

**E1.**
```c
#include <stdio.h>;
int main() { printf("hi"); return 0; }
```
**Error:** stray **semicolon** after `#include`. Preprocessor directives take no `;`.
**Fix:** `#include <stdio.h>`

**E2.**
```c
int main() { int a, b;  scanf("%d%d", a, b); }
```
**Error:** `scanf` needs **addresses**. **Fix:** `scanf("%d%d", &a, &b);`

**E3.**
```c
int x;
scanf("%d", &x);
if (x = 0) printf("zero");
```
**Error:** `=` instead of `==`. The condition assigns 0 and is always false. **Fix:** `if (x == 0)`

**E4.**
```c
float f;
scanf("%f", &f);
printf("%d", f);
```
**Error:** wrong format specifier — `%d` for a `float`. **Fix:** `printf("%f", f);`

**E5.**
```c
double d;
scanf("%f", &d);
```
**Error:** `%f` for a `double` in `scanf`. **Fix:** `scanf("%lf", &d);`

**E6.**
```c
int main() {
    int i = 0, s = 0;
    while (i < 10)
        s = s + i;
    printf("%d", s);
}
```
**Error:** the loop never updates `i` → **infinite loop**. **Fix:** add `i = i + 1;` inside the loop body (and braces).

**E7.**
```c
int a[5];
for (i = 1; i <= 5; i++) a[i] = 0;
```
**Error:** out-of-bounds write — `a[5]` is past the end (valid indices 0…4) and `a[0]` is skipped. **Fix:** `for (i = 0; i < 5; i++)`

**E8.**
```c
int a[5] = {1,2,3,4,5,6};
```
**Error:** more initialisers than the declared size. **Fix:** `int a[6] = {...};` or `int a[] = {...};`

**E9.**
```c
char str[5] = "hello";
```
**Error:** a size-5 array cannot hold `"hello"` plus `'\0'` (6 bytes needed). **Fix:** `char str[6] = "hello";`

**E10.**
```c
int *p;
*p = 10;
```
**Error:** writing through an **uninitialised pointer**. **Fix:** `int x; int *p = &x; *p = 10;` or `p = malloc(sizeof(int));`

**E11.**
```c
int *f() { int t = 5; return &t; }
```
**Error:** returns the address of a **local** variable → dangling pointer. **Fix:** allocate on the heap (`malloc`) or write into a caller-supplied array.

**E12.**
```c
int *p = (int *) malloc(10);
/* intend 10 integers */
```
**Error:** only 10 **bytes** allocated. **Fix:** `malloc(10 * sizeof(int))`.

**E13.**
```c
char *dup(char *s) {
    char *t = malloc(strlen(s));      /* ...copy... */
}
```
**Error:** forgot room for the `'\0'` — needs `strlen(s) + 1`.

**E14.**
```c
void swap(int a, int b) { int t = a; a = b; b = t; }
int main() { int x = 1, y = 2; swap(x, y); }
```
**Error:** call by value — the swap has no effect. **Fix:** parameters must be `int *` and the call `swap(&x, &y)`.

**E15.**
```c
void swap(int *a, int *b) { int *t; t = a; a = b; b = t; }
```
**Error:** swaps the **local pointers**, not the values. **Fix:** `int t = *a; *a = *b; *b = t;`

**E16.**
```c
int gcd(int a, int b) { int t;
    if (a < b) { t = a; a = b; b = a; }   /* exchange */
    ...
}
```
**Error:** the last line of the exchange must be **`b = t;`** — as written `b` gets `a`'s new value.

**E17.**
```c
int fact(int n) { if (n == 1) return 1; return n * fact(n); }
```
**Error:** the recursive call does not make progress (`fact(n)` calls itself with the same `n`) → infinite recursion. **Fix:** `fact(n-1)`.

**E18.**
```c
int fib(int n) { return fib(n-1) + fib(n-2); }
```
**Error:** no base case. **Fix:** `if (n == 0 || n == 1) return 1;`

**E19.**
```c
float f(int a) { return; }
```
**Error:** `return;` with no value in a function that must return a `float` → the returned value is unpredictable.

**E20.**
```c
do {
    scanf("%d", &a);
} while (a != -1)
```
**Error:** missing `;` after `while (a != -1)`. **Fix:** `while (a != -1);`

**E21.**
```c
for (i = 0; i < n; i++);
    printf("%d", i);
```
**Error:** the stray `;` makes the loop body empty; `printf` runs once, after the loop.

**E22.**
```c
switch (x) {
    case 1.5: printf("one and a half"); break;
}
```
**Error:** `float` case label — `switch` requires an **integer** expression and integer constants.

**E23.**
```c
switch (day) {
    case 1: printf("Mon");
    case 2: printf("Tue");
    case 3: printf("Wed");
}
```
**Error:** missing `break`s → **fall-through**; input `1` prints `MonTueWed`.

**E24.**
```c
struct point { int x; int y; }
struct point pt;
```
**Error:** missing `;` after the closing `}` of the structure definition.

**E25.**
```c
struct point *p;
p.x = 5;
```
**Error:** `p` is a pointer; `p.x` is invalid. **Fix:** `p->x = 5;` (or `(*p).x = 5;`) — after pointing `p` at a real structure.

**E26.**
```c
struct point a, b;
if (a == b) printf("same");
```
**Error:** structures cannot be compared with `==`. **Fix:** compare field by field.

**E27.**
```c
FILE *fp = fopen("data.txt", "r");
fscanf(fp, "%d", &x);
```
**Error:** the return of `fopen` is never checked for `NULL`. If `data.txt` does not exist, `fscanf` uses a `NULL` pointer. **Fix:** `if (fp == NULL) { ... }`.

**E28.**
```c
char str[100];
scanf("%s", &str);
```
**Error:** `&str` is a pointer *to the array*; the correct argument is the array itself. **Fix:** `scanf("%s", str);` (`%s` expects `char *`).

**E29.**
```c
int a[10];
b = a;              /* copy the array */
```
**Error:** arrays cannot be assigned. **Fix:** copy element by element in a loop.

**E30.**
```c
printf("%s", 'A');
```
**Error:** `'A'` is a `char`, not a string. **Fix:** `printf("%c", 'A');` or `printf("%s", "A");`

**E31.**
```c
int main() { int i = 5; i = i++ + ++i; printf("%d", i); }
```
**Error:** the same variable is modified twice between sequence points → **undefined behaviour**. There is *no* correct output.

**E32.**
```c
int num[10];
printf("%d", sizeof(num)/sizeof(int));   /* inside a function with int num[] parameter */
```
**Error:** if `num` is a **function parameter** declared as `int num[]`, it is a pointer, so `sizeof(num)` is the pointer size (8) — the element count comes out wrong. **Fix:** pass the length as a separate argument.

---

## 20. Output-prediction drill — Set 1 (with answers)

> Write your trace down before reading the answer. **Wherever you see "undefined", that is a legitimate and frequently correct exam answer.**

**O1.** `printf("%d", 10 - 5 - 15);` → **-10** (`((10-5)-15)`, left-associative).

**O2.** `int a = 10 + 5 * 4 % 2; printf("%d", a);` → **10** (`5*4=20`, `20%2=0`, `10+0`).

**O3.**
```c
int x = 7, y = 2;
printf("%d %d", x/y, x%y);
```
→ **3 1** (integer division truncates).

**O4.**
```c
int i = 5;
printf("%d ", i++);
printf("%d ", i);
printf("%d", ++i);
```
→ **5 6 7** (postfix uses the old value; prefix increments first).

**O5.**
```c
int a = 1, b = 2;
a = a + b;  b = a - b;  a = a - b;
printf("%d %d", a, b);
```
→ **2 1** (the classic swap *without* a temporary).

**O6.**
```c
int i = 0, s = 0;
while (i < 4) { s = s + i; i = i + 1; }
printf("%d", s);
```
→ **6** (`0+1+2+3`).

**O7.**
```c
int i, s = 0;
for (i = 1; i <= 5; i++) s = s + i;
printf("%d", s);
```
→ **15**.

**O8.**
```c
int i = 0, c = 0;
for (i = 0; i < 10; i++) { if (i % 2 == 0) continue; c++; }
printf("%d", c);
```
→ **5** (counts the odd numbers 1,3,5,7,9).

**O9.**
```c
int i;
for (i = 0; i < 10; i++) { if (i == 4) break; }
printf("%d", i);
```
→ **4** (`break` leaves the loop with `i` still 4).

**O10.**
```c
int i = 0;
while (i < 3) { printf("%d ", i); i++; }
```
→ **0 1 2**.

**O11.**
```c
int i = 5;
do { printf("%d ", i); i++; } while (i < 3);
```
→ **5** (a `do-while` body runs at least once).

**O12.**
```c
int i = 0, j;
for (i = 0; i < 3; i++)
    for (j = 0; j < 3; j++)
        printf("*");
```
→ **\*\*\*\*\*\*\*\*\*** (9 stars), the inner loop runs 3×3 = **9** times.

**O13.**
```c
int a[5] = {1,2,3};
int i, s = 0;
for (i = 0; i < 5; i++) s = s + a[i];
printf("%d", s);
```
→ **6** (`1+2+3+0+0` — the rest are initialised to 0).

**O14.**
```c
int num[] = {-2, 3, 5, -7};
printf("%d", num[1] + num[3]);
```
→ **-4** (`3 + (-7)`).

**O15.**
```c
int a[5] = {1,2,3,4,5};
int *p = a;
printf("%d %d", *p, *(p+2));
```
→ **1 3** (`p` points to `a[0]`; `*(p+2)` is `a[2]`).

**O16.**
```c
int a[5] = {1,2,3,4,5};
int *p = &a[0];
p++;
printf("%d", *p);
```
→ **2**.

**O17.**
```c
int a[4] = {10,20,30,40};
int *p = a + 3;
printf("%d", *p - *(p-1));
```
→ **10** (`40 - 30`).

**O18.**
```c
int a[] = {1,2,3,4,5};
printf("%d", (int)(sizeof(a)/sizeof(a[0])));
```
→ **5** (the standard element-count idiom).

**O19.**
```c
char str[] = "I am GR8DON";
printf("%d", (int)strlen(str));
```
→ **11** (the `'\0'` is not counted; `sizeof(str)` would be 12).

**O20.**
```c
char str[] = "I am GR8DON";
str[4] = '\0';
printf("%s", str);
```
→ **`I am`** (`%s` stops at the first `'\0'`).

**O21.**
```c
char str[] = "I am GR8DON";
str[4] = '\0';
int i; for (i = 0; i < 11; i++) putchar(str[i]);
```
→ **`I amGR8DON`** (the `'\0'` prints as nothing; the later characters are still in memory).

**O22.**
```c
char ch;
for (ch = 'A'; ch <= 'F'; ch = ch + 1) printf("%c", ch);
```
→ **`ABCDEF`**.

**O23.**
```c
printf("%c", 'a' - 'a' + 'A');
```
→ **`A`** (arithmetic on ASCII codes).

**O24.**
```c
printf("%d", 'B' - 'A');
```
→ **1** (ASCII 66 - 65).

**O25.**
```c
printf("%d", '9' - '0');
```
→ **9** (the standard digit conversion).

**O26.**
```c
int a = 5;
printf("%d", (int)(a / 2.0 * 2));
```
→ **5** (with a floating-point operand the division is real: `2.5*2 = 5.0` → 5). *Note: `a / 2 * 2` would give **4**.*

**O27.**
```c
printf("%f", (float) 5 / 2);
```
→ **2.500000** (the cast applies to `5`, so real division).

**O28.**
```c
int x = 3;
printf("%d", x++ + ++x);
```
→ **undefined** (the same variable is modified twice — there is no fixed answer).

**O29.**
```c
int x = 3;
printf("%d", x++ + 2);
printf(" %d", x);
```
→ **`5 4`** (no UB here: `x++` is read once).

**O30.**
```c
printf("%d", (1 && 0) + (1 || 0));
```
→ **1** (`0 + 1`).

---

## 20b. Output-prediction drill — Set 2 (with answers)

**O31.**
```c
int f(int a, int b) { return a + b; }
int main() { int a = 1, b = 2;  a = f(a, b);  printf("%d  %d", a, b); }
```
→ **`3  2`** — arguments are copied, so `main`'s `b` is unchanged.

**O32.**
```c
int f(int a, int b) { return a + b; }
int main() { int a = 1, b = 2;  a = f(f(a,b), b);  printf("%d  %d", a, b); }
```
→ **`5  2`** — the inner call is evaluated first: `f(1,2)=3`, then `f(3,2)=5`.

**O33.**
```c
int f(int a, int b) { return b - a; }
int main() { int a = 2, b = 1;  a = f( a=b+1, b=a+1 );  printf("%d %d", a, b); }
```
→ **undefined / compiler dependent** — C does not specify the order of argument evaluation. (Left-to-right gives `1 3`; right-to-left gives `-1 3`.)

**O34.**
```c
void f(int a) { a = 100; }
int main() { int a = 1; f(a); printf("%d", a); }
```
→ **1** — call by value; the change is made to a copy.

**O35.**
```c
void f(int *a) { *a = 100; }
int main() { int a = 1; f(&a); printf("%d", a); }
```
→ **100** — the function writes through the pointer.

**O36.**
```c
int fact(int n) { if (n <= 1) return 1; return n * fact(n-1); }
printf("%d", fact(4));
```
→ **24**.

**O37.**
```c
int fact(int r) { int i, ans = 1;
    for (i = 0; i < r; i = i + 1) ans = ans * (i + 1);
    return ans; }
printf("%d", fact(3));
```
→ **6** (`1*1*2*3`).

**O38.**
```c
int gcd(int a, int b) { if (b == 0) return a; return gcd(b, a % b); }
printf("%d", gcd(102, 21));
```
→ **3** (`102%21=18`, `21%18=3`, `18%3=0` → 3).

**O39.**
```c
int a, b, t, g;
a = 8; b = 6;
while (!(b == 0)) { g = a % b; a = b; b = g; }
printf("%d", a);
```
→ **2**.

**O40.**
```c
int num[10];
int i; for (i = 0; i < 10; i++) num[i] = i*i;
printf("%d", num[4]);
```
→ **16**.

**O41.**
```c
int a = 1; int *p = &a;  a = 5;
printf("%d", *p);
```
→ **5** — `p` follows `a`; it holds the address, not a copy.

**O42.**
```c
struct point { int x; int y; };
struct point pts[3];
int i;
for (i = 0; i < 3; i++) { pts[i].x = i; pts[i].y = i; }
printf("%d", pts[2].y);
```
→ **2**.

**O43.**
```c
struct point { int x; int y; };
struct point pt = {3, 4};
struct point *p = &pt;
printf("%d %d", p->x, (*p).y);
```
→ **3 4**.

**O44.**
```c
struct point { int x; int y; };
struct rect { struct point lb, rt; };
struct rect r;
r.lb.x = 0;  r.rt.y = 1;
printf("%d %d", r.lb.x, r.rt.y);
```
→ **`0 1`** — the `.` operators chain: `r.lb.x` means `(r.lb).x`.

**O45.**
```c
double mat[4][3] = {{1,2,3},{4,5,6},{7,8,9},{0,1,2}};
printf("%f", mat[1][2]);      /* %d would be wrong — the element is a double */
```
→ **6.000000** (row 1, column 2).

**O46.**
```c
int a[][3] = { {1}, {2,3}, {3,4,5} };
printf("%d %d", a[0][2], a[1][1]);
```
→ **0 3**.

**O47.**
```c
int x = 5;
if (x > 3) printf("big"); else printf("small");
```
→ **`big`**.

**O48.**
```c
int x = 2;
switch (x) {
    case 1: printf("one");
    case 2: printf("two");
    case 3: printf("three");
}
```
→ **`twothree`** (fall-through — no `break`).

**O49.**
```c
int x = 5;
switch (x) {
    case 1: printf("one"); break;
    default: printf("other"); break;
}
```
→ **`other`**.

**O50.**
```c
int i = 0;
for (; i < 3; ) { printf("%d", i); i = i + 1; }
```
→ **`012`** (`init` and `update` may be omitted — but the update can also be moved inside the body).

**O51.**
```c
int s = 0, a;
while (scanf("%d", &a) == 1 && a != -1) s = s + a;
/* input: 4 15 -5 -1 */
printf("%d", s);
```
→ **14** (`4 + 15 + (-5)`; the `-1` terminates the loop by the invariant).

**O52.**
```c
int i, s = 0;
for (i = 0; i < 10; i++) { if (i == 5) break; s = s + 1; }
printf("%d", s);
```
→ **5** (`i = 0,1,2,3,4` each add 1).

**O53.**
```c
int n = 5;
while (n-- > 0) printf("%d", n);
```
→ **`43210`** — the test uses `n`'s old value, then decrements.

**O54.**
```c
int a = 3, b = 4;
printf("%f", a / (float) b);
```
→ **0.750000**.

**O55.**
```c
int a = 7, b = 3;
printf("%d %d", a/b, a%b);
```
→ **2 1**.

**O56.**
```c
char *s = "hello";
printf("%c", s[1]);
```
→ **`e`**.

**O57.**
```c
char s[] = "hello";
printf("%c", *(s+4));
```
→ **`o`**.

**O58.**
```c
int a[3] = {1,2,3};
printf("%d", *(a+1) + a[2]);
```
→ **5**.

**O59.**
```c
int i = 1;
printf("%d", i++ * 10);
printf(" %d", i);
```
→ **`10 2`**.

**O60.**
```c
int i;
for (i = 0; i < 5; i = i + 1) ;
printf("%d", i);
```
→ **5** (the empty loop body — note the stray semicolon).

**O61.**
```c
printf("%d", sizeof(char) + sizeof(int));
```
→ **5** (1 + 4, typical machine).

**O62.**
```c
char c = 'A';
printf("%d %c", c, c);
```
→ **`65 A`** — printing the same value as a number and as a character.

---

## 21. Cheat sheet — tables you must be able to recall instantly

### A. Format specifiers
| Specifier | Type | Example output |
|---|---|---|
| `%d` / `%i` | `int` | `42` |
| `%u` | `unsigned int` | `42` |
| `%f` | `float` / `double` in `printf` | `3.140000` |
| `%lf` | `double` in **`scanf`** | — |
| `%e` | scientific | `3.140000e+00` |
| `%c` | `char` | `A` |
| `%s` | string (`char *`) | `hello` |
| `%x` / `%X` | hex | `2a` |
| `%o` | octal | `52` |
| `%ld` / `%lu` | `long` / `unsigned long` | — |
| `%zu` | `size_t` (from `sizeof`) | `4` |
| `%p` | pointer | an address |
| `%%` | literal `%` | `%` |
| `\n` `\t` `\\` `\"` `\0` | newline, tab, backslash, quote, NULL | — |

### B. Operator precedence (high → low) and associativity
| Rank | Operators | Assoc. |
|---|---|---|
| 1 | `()` `[]` `.` `->` (postfix `++` `--`) | L→R |
| 2 | unary `!` `-` `+` `&` `*` `sizeof` `(cast)` `++` `--` | **R→L** |
| 3 | `*` `/` `%` | L→R |
| 4 | `+` `-` | L→R |
| 5 | `<` `<=` `>` `>=` | L→R |
| 6 | `==` `!=` | L→R |
| 7 | `&&` | L→R |
| 8 | `\|\|` | L→R |
| 9 | `?:` | **R→L** |
| 10 | `=` `+=` `-=` `*=` `/=` `%=` | **R→L** |
| 11 | `,` | L→R |

### C. C keywords you have met
`int` `char` `float` `double` `void` `long` `short` `unsigned` `signed` `const` `static`
`if` `else` `switch` `case` `default` `break` `continue` `while` `do` `for` `goto`
`return` `sizeof` `struct` `union` `enum` `typedef`
`extern` `register` `auto` `volatile`

* Not keywords but important: `NULL`, `EOF`, `FILE`, `main`, `stdin`, `stdout`, `stderr`, `SEEK_SET`, `SEEK_CUR`, `SEEK_END`, `size_t`.

### D. Headers and their most-tested functions
| Header | Contents |
|---|---|
| `<stdio.h>` | `printf` `scanf` `getchar` `putchar` `gets` `puts` **`fopen` `fclose` `fscanf` `fprintf` `fgetc` `fputc` `feof` `ferror` `fseek` `ftell`**, `FILE`, `stdin`, `stdout`, `stderr`, `EOF`, `NULL` |
| `<stdlib.h>` | `malloc` `calloc` `realloc` **`free`** `exit` `atoi` `atof` `abs` `rand` `NULL` |
| `<string.h>` | `strlen` `strcpy` `strncpy` `strcat` `strcmp` `strchr` `strstr` |
| `<math.h>` | `sqrt` `pow` `fabs` `sin` `cos` `exp` `log` (link with `-lm`) |
| `<ctype.h>` | `isalpha` `isdigit` `toupper` `tolower` |

### E. Control-flow one-liners
```c
if (c) s1; else s2;              /* non-zero = true */
switch (e) { case k: s; break; default: s; }   /* integer e, unique constant k */
while (e) s;                      /* 0 iterations possible   */
do s; while (e);                  /* >= 1 iteration, needs ; */
for (i=0;i<n;i++) s;              /* init; test; update      */
break;                            /* leave nearest loop/switch */
continue;                         /* skip to next iteration    */
```
* `?:` ternary: `x = (a > b) ? a : b;`
* Comma in `for`: `for (i=0, j=n; i<j; i++, j--)`

### F. Loop counts and complexity
| Pattern | Count |
|---|---|
| `for (i=0; i<n; i++)` | n |
| `for (i=a; i<=b; i++)` | b-a+1 |
| nested n × n | n² |
| triangle of stars | n(n+1)/2 |
| bubble sort comparisons | n(n-1)/2 |
| linear search | n |
| binary search | log₂ n |
| two-way (halving) recursion depth | ~1+log₂ n |
| naive recursive Fibonacci | exponential (≈Fₙ calls) |

### G. Number & ASCII facts
| Fact | Value |
|---|---|
| `'\0'` | 0 |
| `'0'` | 48 |
| `'9'` | 57 |
| `'A'` | 65 |
| `'Z'` | 90 |
| `'a'` | 97 |
| `'z'` | 122 |
| `7/2`, `-7/2` | 3, -3 |
| `7%2`, `-7%2` | 1, -1 |
| `2^10` | 1024 |
| typical sizes | char 1, int 4, float 4, double 8, pointer 8 |

---

## 21b. Equivalences and sizes to remember

> Types, sizes and format specifiers are in **section 2**; the compilation stages and `gcc` commands in **section 1**; file modes and standard streams in **section 14** — they are not repeated here.

### Equivalence table
| Form A | Form B |
|---|---|
| `a[i]` | `*(a+i)` |
| `p->x` | `(*p).x` |
| `mat[i][j]` | `*(*(mat+i)+j)` |
| `&a[0]` | `a` |
| `a[0]` | `*a` |
| `ptr + i` | `ptr + i*sizeof(type)` bytes |
| `i++;` (as a statement) | `++i;` |
| `for (i=0;i<n;i++)` | `i=0; while (i<n) { …; i++; }` |
| `while (expr) stmt` | `for (; expr; ) stmt` |
| `sizeof(a)/sizeof(a[0])` | number of elements |

### Sizes to remember (typical 64-bit machine)
`sizeof(char)=1` · `sizeof(int)=4` · `sizeof(float)=4` · `sizeof(double)=8` · `sizeof(pointer)=8`
`sizeof(int[10])=40` · `sizeof("hello")=6` · `strlen("hello")=5`

---

## 21c. Last-minute facts & self-test checklist

### 1. Undefined behaviour — answer "cannot be determined"
1. `i = i++ + ++i;` (modify twice between sequence points)
2. `a[i] = i++;`
3. `printf("%d %d", i++, i++);` (order unspecified)
4. `f(a = b+1, b = a+1);` (argument evaluation order unspecified)
5. Returning the address of a local variable (dangling pointer)
6. Using a pointer after `free`
7. Writing/reading an array out of bounds
8. Casting a float that does not fit into an `int`
9. `free` twice on the same pointer
10. Reading an **uninitialised** variable
11. `float`-to-`int` when the value is out of range

### 2. Statements that are **not** errors but surprise people
* `if (x = 0)` compiles — it assigns and is false.
* `while (i < n);` compiles — the body is empty.
* `for (;;)` is a legal infinite loop.
* `int num[10] = {1,2,3};` is legal — the rest become 0.
* `char s[] = "abc";` — `sizeof(s)` is 4, `strlen(s)` is 3.
* `main()` without a return type is tolerated by gcc but `int main()` is correct.
* `f(y,x);` ignoring a return value is legal.
* `x = (1,2,3);` assigns **3** (comma operator).
* `printf("%d", 'A');` prints **65**.
* `float` printed with `%f` in `printf` is fine.
* `#define` and `#include` take **no** semicolon.

### 3. One-line facts most likely to be asked
* C is **case-sensitive**; statements end with `;`; `{ }` make a block.
* `0` is false; **any** non-zero value (including `-1`) is true.
* Logical operators **short-circuit**; bitwise ones do not.
* Integer division **truncates**; `%` needs integer operands.
* `=` assigns (right-associative); `==` compares.
* Arrays: indices `0…n-1`, no bounds checking, name decays to a pointer.
* Strings end in `'\0'`; `%s` stops there.
* C is **call by value**; use pointers to modify the caller's data.
* `return expr;` is the only way to send a value back.
* Locals live on the **stack** and die on return; `malloc` gives **heap** memory that survives.
* `sizeof` is an **operator**; it counts **bytes**.
* `fopen` returns `NULL` on failure; modes `r`, `w`, `a`, `r+`, `w+`, `a+`.
* The preprocessor runs **before** the compiler; `<>` = system headers, `""` = your headers.
* Linked lists: one-way navigation; **find-previous** and **insert-before** need a **doubly** linked list.
* `simple_concat` re-links; `deep_concat` copies.

### 4. 10-minute self-test (answers are in 17–20)
1. `printf("%d", 7/2);` → ?
2. `printf("%d", 10-5-15);` → ?
3. `while` vs `do-while`: which runs at least once?
4. `int a[5]={1,2}; printf("%d", a[4]);` → ?
5. `strlen("hello")` and `sizeof("hello")` → ?
6. `int *p; p+1` advances how many bytes?
7. What does `p->x` mean?
8. `mat[i][j]` in pointer form?
9. Which `fopen` mode truncates an existing file?
10. What is the value of `10 % 3` and `-10 % 3`?
11. Name the four compilation stages.
12. Which structure operation is impossible on a singly linked list?
13. What does `#ifndef` guard against?
14. What is the output: `char ch; for (ch='A'; ch<='C'; ch++) printf("%c", ch);`
15. `int i=5; printf("%d", i++);` → ?
16. Is `f(a=b+1, b=a+1)` well-defined?
17. What is the difference between `%f` and `%lf` in `scanf`?
18. What does `feof` return before any read is attempted?
19. `sizeof(a)/sizeof(a[0])` inside a function receiving `int a[]` — reliable?
20. What is the recursion depth of the two-way `max_arr`?

### Answer key
1. 3 · 2. -10 · 3. `do-while` · 4. 0 · 5. 5 and 6 · 6. 4 bytes (one element) · 7. the `x` field of the structure pointed to by `p` (= `(*p).x`) · 8. `*(*(mat+i)+j)` · 9. `"w"` (or `"w+"`) · 10. 1 and **-1** · 11. preprocessor → compiler → assembler → linker · 12. finding the previous node (and inserting before a node) · 13. a header being included twice (redefinition errors) · 14. `ABC` · 15. 5 · 16. No — the argument evaluation order is unspecified · 17. `%f` is for `float`, `%lf` for `double` · 18. 0 (it becomes 1 only after an attempted read past the end) · 19. No — `a` has decayed to a pointer, so `sizeof(a)` is 8 · 20. ≈ 1 + log₂ n.

---

## ⚑ The three rules to read one last time before the exam
1. **Trace, don't guess.** Write the values of every variable after every statement.
2. **If the code has undefined behaviour, the answer is "undefined / compiler dependent".**
3. **Check the small things first:** `;` present? `&` in `scanf`? `=` or `==`? right `%` specifier? index in range? pointer valid?

**Good luck — you have everything you need in this file.** 🎯

*Notes compiled from all 64 `mooc-*.pptx` lecture decks in this folder (NPTEL "Introduction to Programming in C", IIT Kanpur).*


