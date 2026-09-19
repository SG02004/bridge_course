# C Programming – Exam Notes (NPTEL: Introduction to Programming in C)

**Scope:** straight-line code, variables, operators, conditionals, loops, functions, arrays, strings, pointers, recursion, multidimensional arrays, structures, linked lists, files, preprocessor, multi-file projects, makefiles.

> **Golden rule:** Assume standard C. If code has **undefined behavior (UB)**, there is *no guaranteed output*, even if your compiler prints something.

---

## Contents

- [1. MCQ Strategy](#1-mcq-strategy)
- [2. Programming Fundamentals](#2-programming-fundamentals)
- [3. Structure of a C Program](#3-structure-of-a-c-program)
- [4. Tokens & Syntax](#4-tokens--syntax)
- [5. Variables, Constants, Data Types](#5-variables-constants-data-types)
- [6. Type Conversion](#6-type-conversion)
- [7. Input / Output (`<stdio.h>`)](#7-input--output-stdioh)
- [8. Operators & Expressions](#8-operators--expressions)
- [9. Increment / Decrement](#9-increment--decrement)
- [10. Conditionals](#10-conditionals)
- [11. Loops](#11-loops)
- [12. Functions](#12-functions)
- [13. Arrays](#13-arrays)
- [14. Strings](#14-strings)
- [15. Pointers](#15-pointers)
- [16. Recursion](#16-recursion)
- [17. Multidimensional Arrays](#17-multidimensional-arrays)
- [18. Structures & Unions](#18-structures--unions)
- [19. Linked Lists](#19-linked-lists)
- [20. File Handling](#20-file-handling)
- [21. Preprocessor](#21-preprocessor)
- [22. Multiple Source Files](#22-multiple-source-files)
- [23. Makefiles](#23-makefiles)
- [24. Error Categories](#24-error-categories)
- [25. Output-Tracing Method](#25-output-tracing-method)
- [26. High-Yield MCQ Traps](#26-high-yield-mcq-traps)
- [27. Fill-in-the-Blank Table](#27-fill-in-the-blank-table)
- [28. Practice MCQs (with reasoning)](#28-practice-mcqs-with-reasoning)
- [29. One-Page Revision](#29-one-page-revision)
- [Appendix A. Standard Library Quick Reference](#appendix-a-standard-library-quick-reference)
- [Appendix B. Classic Programs (frequently traced in exams)](#appendix-b-classic-programs-frequently-traced-in-exams)
- [Appendix C. Linked List Operations](#appendix-c-linked-list-operations)

---

## 1. MCQ Strategy

| Question type | What to check |
|---|---|
| Output prediction | Precedence, type conversion, loop count, `printf` format, `++`/`--` |
| Find the error | Missing `;`, missing header, wrong format specifier, bad pointer, array bounds |
| Fill in the blank | Keyword, operator, header, library function |
| Conceptual | Scope, storage duration, arrays vs pointers, file modes, recursion |
| Code tracing | Values after every statement, recursion stack |
| Build questions | Preprocessor, compile vs link, header guards, `make` |

### 20 rules that win marks
1. C is case-sensitive.
2. Array indices start at `0`; last element of `a[n]` is `a[n-1]`.
3. `=` assigns, `==` compares.
4. `&&`, `||`, `!` are logical; `&`, `|`, `^`, `~` are bitwise.
5. `i++` uses old value then increments; `++i` increments then uses.
6. Integer / integer = integer (fraction discarded).
7. `scanf` needs addresses (`&x`), except for arrays/strings.
8. Array name usually decays to pointer to first element.
9. C passes arguments **by value**.
10. To modify a caller's variable, pass a pointer.
11. Strings end with `'\0'`.
12. `break` exits nearest loop/`switch`.
13. `continue` skips rest of current iteration.
14. `sizeof` yields `size_t` (print with `%zu`).
15. `fgetc()`/`getchar()` return `int` (to hold `EOF`).
16. `free(NULL)` is safe.
17. Dereferencing `NULL`, uninitialized, dangling pointers = UB.
18. Precedence ≠ order of evaluation.
19. Signed overflow = UB; unsigned wraps.
20. Arrays cannot be assigned with `=`.

---

## 2. Programming Fundamentals

**Pipeline:** Problem → Algorithm → Pseudocode/Flowchart → C source → Preprocess → Compile → Assemble → Link → Executable → Run/Test.

**Algorithm properties:** Input (≥0), Output (≥1), Definiteness, Finiteness, Effectiveness, Correctness, Efficiency.

**Euclid's GCD**
```c
int gcd(int a, int b) {
    while (b != 0) {        // repeat until remainder is 0
        int r = a % b;
        a = b;
        b = r;
    }
    return a;
}
// gcd(48,18): 48%18=12 → 18%12=6 → 12%6=0 → answer 6
```

---

## 3. Structure of a C Program

```c
#include <stdio.h>          // declarations for I/O
int main(void) {            // entry point
    printf("Hello\n");
    return 0;               // 0 = success
}
```

| Term | Meaning |
|---|---|
| Declaration / prototype | Says something exists (`int add(int,int);`) |
| Definition | Provides body / storage |
| Call | Executes the function |

**Translation stages**

| Stage | Task |
|---|---|
| Preprocessing | Expands `#include`, macros, `#if` |
| Compilation | C → assembly/intermediate |
| Assembly | → object code (`.o`) |
| Linking | Combines objects + libraries |
| Loading/Execution | OS loads; CPU runs |

```bash
gcc main.c -o main                  # one step
gcc -c main.c ; gcc -c math.c       # -c = object file, no linking
gcc main.o math.o -o app            # link
```

---

## 4. Tokens & Syntax

Tokens: **keywords** (`int`, `if`), **identifiers**, **constants**, **string literals**, **operators**, **punctuators** (`; , () {} []`).

**Identifier rules:** letters/digits/underscore; cannot start with digit; not a keyword; case-sensitive; no spaces.
Valid: `total`, `student_1`, `_count`. Invalid: `2count`, `student name`, `int`.

**Semicolon trap**
```c
for (int i = 0; i < 5; i++);   // empty loop body!
{ printf("Hello"); }           // runs once, not in loop
```

Comments: `// line`, `/* block */` – removed in preprocessing.

---

## 5. Variables, Constants, Data Types

- Local (automatic) uninitialized variable → **indeterminate** value (don't use).
- Global and `static` variables → **zero-initialized** by default.

| Type | Use |
|---|---|
| `char` | character / small int (`sizeof(char) == 1` always) |
| `short`, `int`, `long`, `long long` | integers (sizes implementation-defined) |
| `float`, `double`, `long double` | reals |
| `_Bool` | boolean |
| `void` | no value/type |

- `unsigned` wraps modulo 2ⁿ. **Signed overflow is UB.**
- Character constant `'A'` has type `int` in C. ASCII: `'0'`=48, `'A'`=65, `'a'`=97.
- Escapes: `\n \t \r \b \\ \' \" \0 \a`.

**Literals:** `10` int, `10U` unsigned, `10L` long, `10LL` long long, `3.14` double, `3.14f` float, `3.14L` long double.

**Constants:** `const int n = 5;` (typed, read-only) · `#define MAX 100` (macro, no type) · `enum Day {MON, TUE, WED};` → 0, 1, 2.

---

## 6. Type Conversion

```c
int    x = 5 / 2;        // 2
double y = 5 / 2;        // 2.0  (division done in int first!)
double z = 5.0 / 2;      // 2.5
double w = (double)5/2;  // 2.5
int    c = (int)3.99;    // 3   (truncates toward zero)
int    d = (int)-3.99;   // -3
```

- Promotion order: `long double > double > float > integer types`.
- `char`/`short` are promoted to `int` in expressions.
- `float` passed to `printf` is promoted to `double`.

---

## 7. Input / Output (`<stdio.h>`)

### `printf` specifiers
| Spec | Argument | Spec | Argument |
|---|---|---|---|
| `%d` `%i` | int | `%f` | double |
| `%u` | unsigned | `%e` / `%g` | double |
| `%ld` / `%lld` | long / long long | `%c` | int (char) |
| `%x` / `%o` | unsigned hex/octal | `%s` | char* (string) |
| `%zu` | size_t | `%p` | `(void*)` pointer |
| `%%` | literal `%` | | |

### `scanf` specifiers (need pointers)
| Spec | Argument | Spec | Argument |
|---|---|---|---|
| `%d` | `int *` | `%lf` | `double *` |
| `%f` | `float *` | `%c` | `char *` |
| `%ld` | `long *` | `%s` | `char *` (array) |

**Key trap:** `scanf("%f",&f)` for float, `scanf("%lf",&d)` for double, but `printf("%f", d)` for both.

**Mistakes**
```c
scanf("%d", x);          // WRONG: missing &
scanf("%d", &x);         // right
scanf("%19s", name);     // right (array decays; width prevents overflow)
scanf("%19s", &name);    // wrong style
scanf(" %c", &ch);       // leading space skips whitespace/newline
```

- `%c` does **not** skip whitespace; `%s`, `%d` do.
- `%s` reads until whitespace, appends `'\0'`; unbounded → overflow.
- `scanf` returns number of items successfully assigned: `if (scanf("%d",&x) == 1)`.
- `getchar()` returns `int`; `putchar(c)` writes one char.
- `puts(s)` adds newline; `fputs(s, stdout)` does not.
- `printf` **returns the number of characters printed** (`printf("%d", printf("Hi"))` → `Hi2`).

### `printf` width, precision, flags
| Format | Meaning | Example → output |
|---|---|---|
| `%5d` | width 5, right-justified | `42` → `   42` |
| `%-5d` | width 5, left-justified | `42` → `42   ` |
| `%05d` | zero-padded | `42` → `00042` |
| `%+d` | always show sign | `42` → `+42` |
| `%.2f` | 2 digits after the point | `3.14159` → `3.14` |
| `%8.3f` | width 8, 3 decimals | `3.14159` → `   3.142` |
| `%.3s` | at most 3 chars of a string | `"abcdef"` → `abc` |
| `%x` / `%X` / `%o` | hex (lower/upper) / octal | `255` → `ff` / `FF` / `377` |
| `%c` with int | prints the character | `65` → `A` |
| `%d` with char | prints the code | `'A'` → `65` |
| `%f` with no precision | 6 decimals | `2.5` → `2.500000` |

---

## 8. Operators & Expressions

| Group | Operators |
|---|---|
| Arithmetic | `+ - * / %` (`%` needs integers; `7 % 3 = 1`) |
| Relational | `< > <= >= == !=` → result 0 or 1 |
| Logical | `&&` `\|\|` `!` (0 = false, nonzero = true) |
| Bitwise | `&` `\|` `^` `~` `<<` `>>` |
| Assignment | `= += -= *= /= %=` (right-to-left) |
| Conditional | `c ? a : b` |
| Comma | `x = (1,2,3);` → 3 |
| sizeof | bytes, type `size_t` |

**Short-circuit:** `A && B` – B evaluated only if A true. `A || B` – B evaluated only if A false.
```c
if (p != NULL && *p == 10) { ... }   // safe: no deref when p is NULL
```

**Bitwise example:** `5 = 0101`, `3 = 0011` → `5&3 = 1`, `5|3 = 7`, `5^3 = 6`.

**Chained assignment:** `y = x = 10;` → both 10.

**`sizeof`**
```c
int a[5];
sizeof(a)                    // total bytes of array
sizeof(a) / sizeof(a[0])     // number of elements (only for true arrays, not params)
```

### Precedence (high → low)
| Level | Operators | Assoc. |
|---:|---|---|
| 1 | `() [] . ->` postfix `++ --` | L→R |
| 2 | prefix `++ --`, unary `+ -`, `! ~ * & sizeof` | R→L |
| 3 | `* / %` | L→R |
| 4 | `+ -` | L→R |
| 5 | `<< >>` | L→R |
| 6 | `< <= > >=` | L→R |
| 7 | `== !=` | L→R |
| 8 | `&` | L→R |
| 9 | `^` | L→R |
| 10 | `\|` | L→R |
| 11 | `&&` | L→R |
| 12 | `\|\|` | L→R |
| 13 | `?:` | R→L |
| 14 | `= += -= ...` | R→L |
| 15 | `,` | L→R |

`2 + 3 * 4 = 14`.

### Precedence ≠ evaluation order
`f() + g()` – C does not fix which runs first. These are **UB**:
```c
i = i++ + 1;
i = ++i + i++;
printf("%d %d", i++, i++);
```

### Handy facts that show up in MCQs
- **Negative division:** `/` truncates toward zero; `%` takes the sign of the **dividend** → `-7/2 = -3`, `-7%2 = -1`, `7%-2 = 1`.
- **Literals:** `010` is octal (= 8), `0x1F` is hex (= 31).
- **Char arithmetic:** `'a' - 'A' = 32`; `ch - '0'` converts a digit char to its int value; `'a' + 1` is `'b'`.
- **Bit tricks:** `x & 1` tests odd; `1 << n` = 2ⁿ; `x >> 1` = `x / 2` for non-negative `x`.
- **Float comparison:** `0.1 + 0.2 == 0.3` is false (rounding). Compare with a tolerance.
- `%` on floating-point operands is a **compile error** (use `fmod`).

---

## 9. Increment / Decrement

```c
int x = 5; int y = x++;   // y=5, x=6
int x = 5; int y = ++x;   // x=6, y=6
```

| Expression | Meaning |
|---|---|
| `*p++` | `*(p++)` – deref, then move pointer |
| `(*p)++` | increment pointed value |
| `++*p` | `++(*p)` – increment pointed value first |
| `*++p` | move pointer first, then deref |

---

## 10. Conditionals

- Any nonzero value is true (`if (5)` executes).
- **Dangling else:** `else` binds to the nearest unmatched `if`. Use braces.
- **Trap:** `if (x = 0)` assigns 0 → false. `if (x = 5)` → true. Intentional form: `if ((ch = getchar()) != EOF)`.

### `switch`
- Controlling expression: integral/char/enum. `case` labels: **constant** integral expressions, no duplicates.
- Without `break`, execution **falls through**.
```c
int x = 2;
switch (x) {
    case 1: printf("A");
    case 2: printf("B");     // starts here
    case 3: printf("C"); break;
}
// Output: BC
```
- `break` exits only the nearest `switch`/loop.

---

## 11. Loops

| Loop | Behaviour |
|---|---|
| `while (c) {}` | test first; may run 0 times |
| `do {} while (c);` | runs ≥ 1 time; **semicolon required** |
| `for (init; cond; update)` | order: init → cond → body → update → cond … |

- `for (;;)` = infinite loop (missing condition = true).
- `continue`: in `for`, jumps to **update**; in `while`, jumps to **condition**.
- `break` exits nearest loop only.
- Nested loops: body runs `m × n` times.

```c
for (int i = 0; i < 5; i++) { if (i == 2) continue; printf("%d", i); }  // 0134
for (int i = 0; i < 10; i++) { if (i == 4) break;    printf("%d", i); }  // 0123
```

**Common errors:** missing update (infinite loop), `i <= n` off-by-one (runs n+1 times; invalid index for array of size n), `while(cond);` empty body.

---

## 12. Functions

```c
int square(int x);             // prototype
int square(int x) { return x*x; }   // definition
int r = square(5);             // call
```

- `void f(void)` = takes no arguments. `void f()` = unspecified parameters (old style).
- **Pass by value:**
```c
void change(int x)  { x = 100; }    // caller's variable unchanged → prints 5
void change(int *x) { *x = 100; }   // change(&a) → prints 100
```
- Non-`void` function missing `return` → UB if result used.
- Local variable: block scope. Local hides global of same name (**shadowing**).
- **`static` local:** initialized once, keeps value between calls, program lifetime, local scope.
```c
void counter(void){ static int c = 0; c++; printf("%d ", c); }
// three calls → 1 2 3
```
- Global variable: file scope, external linkage. `static` at file scope → visible only in that file.
- `extern int total;` declares a variable defined elsewhere.

### Storage classes
| Class | Scope | Lifetime | Default init |
|---|---|---|---|
| `auto` (default for locals) | block | until block ends | garbage |
| `register` | block | until block ends | garbage (cannot take `&`) |
| `static` (local) | block | whole program | 0 |
| `static` (file scope) | this file only | whole program | 0 |
| `extern` / global | file / other files | whole program | 0 |

---

## 13. Arrays

```c
int a[5];                      // indices 0..4
int a[5] = {1, 2};             // 1 2 0 0 0
int a[5] = {0};                // all zeros
int a[]  = {10, 20, 30};       // size 3
```

- `a[3]` on a 3-element array = **UB** (no bounds checking).
- `a` decays to `&a[0]` except in `sizeof(a)` and `&a`.
- `&a` has type `int (*)[5]`.
- `a[i] == *(a+i) == i[a]`.
- Array parameter `int a[]` ≡ `int *a` → `sizeof(a)` inside the function = **pointer size**. Always pass length separately.
- Arrays passed to functions can be modified by the callee (pointer to first element).

---

## 14. Strings

```c
char word[] = "cat";      // 'c' 'a' 't' '\0' → 4 bytes
```

| Expression | `char s[]="abc"` |
|---|---:|
| `strlen(s)` | 3 |
| `sizeof(s)` | 4 |
| `sizeof("abc")` | 4 |

- `char s[3] = "abc";` legal but **no `'\0'`** → not a string; `printf("%s", s)` is UB.
- `char a[] = "hello";` → modifiable copy.
- `char *p = "hello"; p[0]='H';` → **UB** (string literal).

**`<string.h>`:** `strlen`, `strcpy`, `strncpy`, `strcat`, `strcmp`, `strchr`, `strstr`, `memcpy` (no overlap), `memmove` (overlap safe), `memset`.
`strcmp` → 0 equal, negative if first smaller, positive if larger (**not necessarily ±1**).

Input: `scanf("%19s", name)` reads one word; `fgets(name, sizeof name, stdin)` reads a line (may keep `'\n'`).

---

## 15. Pointers

```c
int x = 10;
int *p = &x;        // p holds address of x
*p = 20;            // x becomes 20
```

| Expr | Meaning |
|---|---|
| `x` | value |
| `&x` | address |
| `p` | stored address |
| `*p` | value at address |

- `int *p, q;` → only `p` is a pointer. Use `int *p, *q;`.
- Uninitialized pointer deref (`int *p; *p = 10;`) → UB. `NULL` deref → UB.
- **Pointer arithmetic** scales by type size: `p + 1` = next `int`. Valid within an array and one-past-end (don't dereference one-past-end). `&a[4] - &a[1] = 3`.
- Pointer to pointer: `int **pp = &p;` → `**pp == x`.

### `const` with pointers
| Declaration | Can change `*p`? | Can change `p`? |
|---|:-:|:-:|
| `const int *p` | No | Yes |
| `int *const p` | Yes | No |
| `const int *const p` | No | No |

### Dynamic memory (`<stdlib.h>`)
```c
int *p = malloc(5 * sizeof *p);        // uninitialized
if (p == NULL) { /* allocation failed */ }
int *q = calloc(5, sizeof *q);         // zero-initialized
int *t = realloc(p, 10 * sizeof *p);   // use temp pointer
if (t != NULL) p = t;
free(p); p = NULL;
```
- **Use-after-free** and **double free** = UB. `free(NULL)` safe.
- Returning address of a local variable = dangling pointer. Safe alternatives: heap memory, `static` object, pointer passed in.

---

## 16. Recursion

Needs: **base case**, **recursive case**, **progress toward base**.

```c
int factorial(int n) { return n == 0 ? 1 : n * factorial(n - 1); }
int fib(int n)       { return n <= 1 ? n : fib(n-1) + fib(n-2); }   // exponential time
```

**Output-order trace**
```c
void f(int n) {
    if (n == 0) return;
    printf("%d", n);     // executes going DOWN
    f(n - 1);
    printf("%d", n);     // executes while RETURNING
}
// f(3) → 321123     f(2) → 2112
```

- No base case → stack exhaustion.
- Each call has its own stack frame (parameters, locals, return address).

---

## 17. Multidimensional Arrays

```c
int m[2][3] = { {1,2,3}, {4,5,6} };
```
- Stored **row-major**: `1 2 3 4 5 6`.
- `m` decays to `int (*)[3]`. `m[i][j] == *(*(m+i)+j)`.
- `*(*(m+1)+2)` = `m[1][2]` = **6**.
- Function parameter needs column size: `void f(int a[][3], int rows)` ≡ `int (*a)[3]`.
- `int **a` is **not** compatible with a 2-D array.

---

## 18. Structures & Unions

```c
struct Student { char name[20]; int marks; };
struct Student s = {"Asha", 95};
struct Student *p = &s;
s.marks;   p->marks;   (*p).marks;     // last two are equivalent
```

- `.` for object, `->` for pointer to struct.
- `typedef struct Node { int data; struct Node *next; } Node;`
- **Self-reference:** allowed only via **pointer** (`struct Node *next`). Containing `struct Node next` is invalid (infinite size).
- Structure assignment `b = a;` copies members (including arrays inside).
- Structures **cannot** be compared with `==`; compare members.
- `sizeof(struct)` may exceed sum of members (**padding**).
- **Union:** members share memory; one active member at a time; size ≥ largest member.

---

## 19. Linked Lists

```c
struct Node { int data; struct Node *next; };
struct Node *head = NULL;              // empty list: head == NULL

struct Node *create_node(int v) {
    struct Node *n = malloc(sizeof *n);
    if (n == NULL) return NULL;
    n->data = v; n->next = NULL;
    return n;
}

void print_list(struct Node *head) {
    for (struct Node *cur = head; cur != NULL; cur = cur->next)
        printf("%d ", cur->data);
}

void push_front(struct Node **head, int v) {   // ** because head itself changes
    struct Node *n = create_node(v);
    if (n == NULL) return;
    n->next = *head;
    *head = n;
}
```

| | Singly | Doubly |
|---|---|---|
| Links | `next` | `prev`, `next` |
| Backward traversal | No | Yes |
| Memory | Less | More |
| Delete given node | Needs previous | Easier |

Doubly insert: update **both** directions (`prev->next`, `new->prev`, `new->next`, `next->prev`).

---

## 20. File Handling

```c
FILE *fp = fopen("data.txt", "r");
if (fp == NULL) { printf("Unable to open file\n"); }
fclose(fp);
```

| Mode | Meaning |
|---|---|
| `"r"` | read; file must exist |
| `"w"` | write; **creates or truncates** |
| `"a"` | append at end; creates if needed |
| `"r+"` | read/write existing |
| `"w+"` | read/write; truncates/creates |
| `"a+"` | read + append |
| `"rb"` / `"wb"` | binary read / write |

**Correct read loop**
```c
int ch;                                   // int, NOT char
while ((ch = fgetc(fp)) != EOF) putchar(ch);
```
- `while (!feof(fp))` is **wrong**: EOF flag is set only *after* a read fails.
- After the loop: `ferror(fp)` = read error; `feof(fp)` = normal end.
- Formatted: `fprintf(fp, "%d %s\n", n, name);` `fscanf(fp, "%d", &n);`
- Lines: `while (fgets(line, sizeof line, fp) != NULL)`.
- Binary: `fread(buf, sizeof *buf, count, fp)` / `fwrite(...)`.
- Position: `fseek`, `ftell`, `rewind`, `fgetpos`, `fsetpos`.
- `fputc` writes a char; `fputs` writes a string.

---

## 21. Preprocessor

- `#include <x.h>` → system headers; `#include "x.h"` → project headers.
- `#define MAX 100` → text replacement.
- **Macro parentheses:**
```c
#define SQ(x)  x * x         // SQ(1+2) → 1 + 2 * 1 + 2 = 5  (wrong)
#define SQ(x)  ((x) * (x))   // SQ(1+2) → 9  (right)
SQ(i++)                       // expands to ((i++)*(i++)) → UB
```
- **Header guard**
```c
#ifndef MATH_UTIL_H
#define MATH_UTIL_H
int add(int a, int b);
#endif
```
- Conditional compilation: `#ifdef DEBUG … #endif`, `#if VERSION >= 2 … #else … #endif`.

---

## 22. Multiple Source Files

```
project/
├── include/mathutil.h
├── src/main.c
├── src/mathutil.c
└── Makefile
```
- `.h` → declarations + guards; `.c` → definitions; `main.c` includes the header.
```bash
gcc -Wall -Wextra -std=c17 -Iinclude -c src/mathutil.c -o mathutil.o
gcc -Wall -Wextra -std=c17 -Iinclude -c src/main.c -o main.o
gcc main.o mathutil.o -o app
```

| Error kind | Example |
|---|---|
| Compiler | syntax error, unknown type, missing `;` |
| Linker | `undefined reference to 'add'` (declared but object file not linked) |

---

## 23. Makefiles

```make
CC = gcc
CFLAGS = -Wall -Wextra -std=c17 -Iinclude

app: main.o mathutil.o
	$(CC) main.o mathutil.o -o app

main.o: src/main.c include/mathutil.h
	$(CC) $(CFLAGS) -c src/main.c -o main.o

mathutil.o: src/mathutil.c include/mathutil.h
	$(CC) $(CFLAGS) -c src/mathutil.c -o mathutil.o

clean:
	rm -f app main.o mathutil.o

.PHONY: clean
```
- Format: `target: prerequisites` then command lines.
- Commands must begin with a **TAB**.
- `make` rebuilds a target only if a prerequisite is newer.
- `.PHONY` = target is not a real file.

---

## 24. Error Categories

| Category | Example |
|---|---|
| Syntax | `int x = 10` (missing `;`) |
| Semantic / constraint | `a = b;` for arrays |
| Linker | `undefined reference` |
| Runtime | segfault, division by zero, failed `fopen` use |
| Logical | `if (x = 5)` instead of `==` |
| **Undefined behavior** | see checklist below |

---

## 25. Output-Tracing Method

1. Add parentheses to complex expressions.
2. Write initial values of all variables.
3. Execute one statement at a time.
4. Treat pre/post increment separately.
5. Count loop iterations.
6. Track spaces and newlines exactly.
7. Check integer vs floating division.
8. Check value vs address passing.
9. Check array indices.
10. On UB → answer "undefined".

**Worked examples**
```c
// 1) Increments
int x = 5;
printf("%d ", x++);   // 5   (x=6)
printf("%d ", ++x);   // 7   (x=7)
printf("%d", x);      // 7        → 5 7 7

// 2) Sum
int sum = 0;
for (int i = 1; i <= 4; i++) sum += i;   // 1,3,6,10 → 10

// 3) Division
printf("%d %.1f", 5/2, 5/2.0);           // 2 2.5

// 4) String size
char s[] = "C";
printf("%zu %zu", strlen(s), sizeof(s)); // 1 2
```

---

## 26. High-Yield MCQ Traps

1. `if (x = 10)` assigns and is true.
2. `scanf` uses `%f` for `float` but `%lf` for `double`; `printf` uses `%f` for both.
3. `sizeof` on an array parameter gives pointer size.
4. Arrays cannot be assigned: use a loop or `memcpy(a, b, sizeof a)`.
5. `char s[3] = {'a','b','c'};` is **not** a string.
6. `sizeof(i++)` does **not** evaluate `i++` (i unchanged).
7. `continue` in `for` → goes to update expression.
8. `break` in nested loop exits only the inner loop.
9. `fgetc` result must be `int`.
10. `p->x` for pointer, `n.x` for object (`n->x` on object is an error).
11. `int *p, q;` → `q` is a plain `int`.
12. `i = i++ + 1;` and `printf("%d %d", i++, i++)` → **UB**.
13. `void f()` ≠ `void f(void)`.
14. `strcmp` result is not necessarily ±1.
15. `"w"` mode destroys existing content.

---

## 27. Fill-in-the-Blank Table

| Blank | Answer |
|---|---|
| Header for `printf`/`scanf` | `<stdio.h>` |
| Header for `malloc`/`free` | `<stdlib.h>` |
| Header for `strlen`/`strcmp` | `<string.h>` |
| Address-of / dereference | `&` / `*` |
| Struct member (object / pointer) | `.` / `->` |
| String terminator | `'\0'` |
| End-of-file constant | `EOF` |
| Null pointer | `NULL` |
| Allocate / zero-allocate / resize / free | `malloc` / `calloc` / `realloc` / `free` |
| Open / close file | `fopen` / `fclose` |
| Read / write one char (file) | `fgetc` / `fputc` |
| Read a line / write a string | `fgets` / `fputs` |
| Size operator | `sizeof` |
| Macro directive | `#define` |
| Header guard start / end | `#ifndef` / `#endif` |
| Compile-only gcc flag | `-c` |
| Entry function | `main` |
| No-parameter list | `(void)` |
| Exit loop / skip iteration | `break` / `continue` |
| Structure / type alias | `struct` / `typedef` |
| External declaration / persistent local | `extern` / `static` |

---

## 28. Practice MCQs (with reasoning)

### 28.1 Output prediction

**O1.**
```c
int x = 5;
printf("%d %d %d", x++, ++x, x);
```
A. `5 7 7` · B. `5 6 7` · C. Undefined behavior · D. Compile error  
**Ans: C** – `x` is modified and read with no sequencing between the arguments.

**O2.**
```c
int x = 5;
printf("%d ", x++);   // prints 5, x = 6
printf("%d ", ++x);   // x = 7, prints 7
printf("%d", x);      // prints 7
```
A. `5 6 6` · B. `5 7 7` · C. `6 6 7` · D. `7 7 7`  
**Ans: B**

**O3.** `printf("%d %d", -7 / 2, -7 % 2);`  
A. `-4 -1` · B. `-3 -1` · C. `-3 1` · D. `-4 1`  
**Ans: B** – division truncates toward zero; `%` takes the sign of the dividend.

**O4.**
```c
int x = 2;
switch (x) {
    case 1: printf("A");
    case 2: printf("B");
    case 3: printf("C"); break;
}
```
A. `A` · B. `B` · C. `BC` · D. No output  
**Ans: C** – no `break` after case 2, so it falls through into case 3.

**O5.**
```c
int i = 0;
while (i < 3) {
    if (i == 1) { i++; continue; }   // skips the printf when i == 1
    printf("%d", i);
    i++;
}
```
A. `012` · B. `02` · C. `01` · D. Infinite loop  
**Ans: B**

**O6.** `char s[] = "abc"; printf("%zu %zu", strlen(s), sizeof(s));`  
A. `3 3` · B. `4 4` · C. `3 4` · D. `4 3`  
**Ans: C** – `strlen` excludes `'\0'`, `sizeof` includes it.

**O7.**
```c
void change(int x) { x = 100; }
int main(void) { int x = 10; change(x); printf("%d", x); }
```
A. `10` · B. `100` · C. UB · D. Compile error  
**Ans: A** – pass by value; only the copy changes.

**O8.**
```c
void f(void) { static int x; printf("%d ", ++x); }
// main calls f() three times
```
A. `1 1 1` · B. `0 0 0` · C. `1 2 3` · D. UB  
**Ans: C** – `static` persists and starts at 0.

**O9.**
```c
void f(int n) {
    if (n == 0) return;
    printf("%d", n);
    f(n - 1);
    printf("%d", n);
}
// f(2)
```
A. `21` · B. `1221` · C. `2112` · D. `2211`  
**Ans: C** – prints `2`, recurses (prints `1`, recurses, prints `1`), then prints `2`.

**O10.** `int a[2][3] = {{1,2,3},{4,5,6}}; printf("%d", *(*(a + 1) + 2));`  
A. `3` · B. `4` · C. `5` · D. `6`  
**Ans: D** – equals `a[1][2]`.

**O11.**
```c
int i = 5;
int s = sizeof(i++);
printf("%d", i);
```
A. `4` · B. `5` · C. `6` · D. UB  
**Ans: B** – `sizeof` does not evaluate its operand.

**O12.** `printf("%d", 10 + 2 * 3 % 4);`  
A. `10` · B. `11` · C. `12` · D. `16`  
**Ans: C** – `*` and `%` are same level, left to right: `(2*3)%4 = 2`, then `10 + 2`.

**O13.**
```c
int a = 0, b = 0;
if (a++ && b++) { }
printf("%d %d", a, b);
```
A. `0 0` · B. `1 0` · C. `1 1` · D. UB  
**Ans: B** – `a++` yields 0 (false), so `b++` is short-circuited.

**O14.**
```c
#define SQ(x) x * x
printf("%d", SQ(2 + 3));
```
A. `25` · B. `11` · C. `10` · D. `15`  
**Ans: B** – expands to `2 + 3 * 2 + 3 = 11`.

**O15.** `printf("%d", printf("Hi"));`  
A. `Hi` · B. `2` · C. `Hi2` · D. `Hi3`  
**Ans: C** – inner `printf` prints `Hi` and returns 2 (characters printed).

**O16.**
```c
int a[] = {10, 20, 30};
int *p = a + 1;
printf("%d %d", *(p - 1), p[1]);
```
A. `10 30` · B. `20 30` · C. `10 20` · D. `20 10`  
**Ans: A**

**O17.**
```c
int i = 5;
do { printf("%d", i); } while (i < 5);
```
A. No output · B. `5` · C. `55` · D. Infinite loop  
**Ans: B** – `do-while` runs the body once before testing.

**O18.** `printf("%c %d", 'a' + 1, 'A' + 1);` (ASCII)  
A. `b 66` · B. `b 98` · C. `98 66` · D. `a 65`  
**Ans: A**

**O19.** `printf("%5d|%-5d|%05d", 42, 42, 42);`  
A. `42|42|42` · B. `   42|42   |00042` · C. `42   |   42|00042` · D. `   42|   42|00042`  
**Ans: B** – width 5 right-justified; `-` left-justified; `0` zero-pads.

### 28.2 Find the error

| # | Code | Error and fix |
|---|---|---|
| E1 | `int x; scanf("%d", x);` | Missing address → UB. Use `&x`. |
| E2 | `int a[3], b[3]; a = b;` | Arrays are not assignable (compile error). Loop or `memcpy`. |
| E3 | `struct Node n; n->data = 5;` | `->` needs a pointer (compile error). Use `n.data`. |
| E4 | `char *s = "abc"; s[0] = 'A';` | Modifying a string literal → UB. Use `char s[] = "abc";`. |
| E5 | `while (!feof(fp)) { ch = fgetc(fp); putchar(ch); }` | Extra iteration with `EOF`. Use `while ((ch = fgetc(fp)) != EOF)`. |
| E6 | `#define MAX 100;` then `int a[MAX];` | Expands to `int a[100;];` → syntax error. No `;` in macros. |
| E7 | `struct P { int x; }` (no `;`) followed by `int main(void)` | Missing `;` after struct definition → compile error. |
| E8 | `int *p = malloc(5); p[4] = 1;` | Allocates 5 **bytes**, not 5 ints → UB. Use `5 * sizeof *p`. |
| E9 | `free(p); free(p);` | Double free → UB. Set `p = NULL` after `free`. |
| E10 | `int *f(void) { int x = 10; return &x; }` | Returns address of a local → dangling pointer. |

### 28.3 Fill in the blanks

| # | Code | Answer |
|---|---|---|
| F1 | `fopen("log.txt", ___)` to append | `"a"` |
| F2 | `struct Node *n = malloc(sizeof(___));` | `struct Node` (or `*n`) |
| F3 | Reverse list: `next = cur->next; cur->next = ___; prev = cur; cur = next;` | `prev` |
| F4 | `strcmp(a, b) == ___` when strings are equal | `0` |
| F5 | `#___ UTIL_H` / `#define UTIL_H` (header guard) | `ifndef` |
| F6 | `for (i = 0; i < sizeof(a) / ___; i++)` | `sizeof(a[0])` |
| F7 | `int m[4][5];` → `void f(int a[][___], int rows)` | `5` |
| F8 | `while ((ch = ___(stdin)) != EOF)` | `getchar` |
| F9 | `void swap(int *a, int *b) { int t = ___; *a = *b; *b = t; }` | `*a` |

### 28.4 Conceptual

- **C1.** `sizeof` on an array parameter (`void f(int a[])`) gives → **pointer size**.
- **C2.** `calloc` differs from `malloc` because it **zero-initializes** the memory.
- **C3.** `undefined reference to 'add'` occurs at the **linking** stage.
- **C4.** `fopen("x.txt", "r")` on a missing file returns **`NULL`**.
- **C5.** `malloc` memory lives on the **heap**; ordinary local variables live on the **stack**.
- **C6.** `const int *p` → cannot change `*p`, can change `p`. `int *const p` → can change `*p`, cannot change `p`.
- **C7.** The loop guaranteed to run at least once is **`do-while`**.
- **C8.** `void f()` = unspecified parameters; `void f(void)` = no parameters.

---

## 29. One-Page Revision

```c
#include <stdio.h>
int main(void) { return 0; }

scanf("%d", &x);   printf("%d", x);
scanf("%f", &f);   scanf("%lf", &d);   printf("%f", d);

while (c) {}   do {} while (c);   for (i; c; u) {}

int a[5];              // 0..4        a[i] == *(a+i)
char s[] = "abc";      // strlen 3, sizeof 4

int x = 10; int *p = &x; *p = 20;

struct Node { int data; struct Node *next; };   // node.data ; ptr->data

int *p = malloc(n * sizeof *p);
if (p != NULL) { /* use */ }
free(p); p = NULL;

FILE *fp = fopen("data.txt", "r");
if (fp != NULL) { int ch; while ((ch = fgetc(fp)) != EOF) putchar(ch); fclose(fp); }
```

**Precedence memory line:** `* / %` → `+ -` → `< <= > >=` → `== !=` → `&&` → `||` → `?:` → `=`

### Undefined-Behavior Checklist (check BEFORE choosing an output)
- [ ] Array index out of bounds
- [ ] Division by zero
- [ ] Signed integer overflow
- [ ] Uninitialized variable read
- [ ] NULL / uninitialized / dangling pointer dereference
- [ ] Use-after-free, double free
- [ ] Modifying a string literal
- [ ] Missing string terminator
- [ ] Unsequenced modifications (`i++ + ++i`)
- [ ] Returning address of a local variable
- [ ] Wrong format specifier for argument type
- [ ] Using a `FILE *` from a failed `fopen`
- [ ] Modifying a `const` object
- [ ] `%d` used for a `size_t` (use `%zu`)

**Highest-priority revision topics:** loops, arrays, pointers, recursion, multidimensional arrays, structures, linked lists, files.

---

## Appendix A. Standard Library Quick Reference

| Header | Functions / items |
|---|---|
| `<ctype.h>` | `isdigit`, `isalpha`, `isalnum`, `isupper`, `islower`, `isspace`, `toupper`, `tolower` |
| `<math.h>` | `sqrt`, `pow`, `fabs`, `ceil`, `floor`, `round` (link with `-lm` on Linux) |
| `<stdlib.h>` | `malloc`, `calloc`, `realloc`, `free`, `exit`, `abs`, `atoi`, `rand`, `srand`, `qsort` |
| `<string.h>` | `strlen`, `strcpy`, `strcat`, `strcmp`, `strchr`, `strstr`, `memcpy`, `memmove`, `memset` |
| `<limits.h>` | `INT_MAX`, `INT_MIN`, `CHAR_BIT` |
| `<stdbool.h>` | `bool`, `true`, `false` |
| `<stddef.h>` | `size_t`, `NULL` |

Notes: `abs` is in `<stdlib.h>`, `fabs` is in `<math.h>`. `ceil(2.1) = 3.0`, `floor(-2.1) = -3.0`. `pow` and `sqrt` return `double`.

---

## Appendix B. Classic Programs (frequently traced in exams)

```c
/* Swap using pointers */
void swap(int *a, int *b) { int t = *a; *a = *b; *b = t; }

/* Reverse an array in place */
void reverse(int a[], int n) {
    for (int i = 0, j = n - 1; i < j; i++, j--) {   // two indices meet in the middle
        int t = a[i]; a[i] = a[j]; a[j] = t;
    }
}

/* Prime check: test divisors up to sqrt(n) */
int is_prime(int n) {
    if (n < 2) return 0;
    for (int i = 2; i * i <= n; i++)
        if (n % i == 0) return 0;
    return 1;
}

/* Reverse digits / palindrome number */
int reverse_num(int n) {
    int r = 0;
    while (n > 0) { r = r * 10 + n % 10; n /= 10; }
    return r;                    // n is palindrome if reverse_num(n) == n
}

/* Binary search on a sorted array; returns index or -1 */
int bsearch_int(int a[], int n, int key) {
    int lo = 0, hi = n - 1;
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;      // avoids overflow of lo + hi
        if (a[mid] == key) return mid;
        if (a[mid] < key) lo = mid + 1; else hi = mid - 1;
    }
    return -1;
}

/* Bubble sort: after pass k, the k largest values are in place */
void bubble(int a[], int n) {
    for (int i = 0; i < n - 1; i++)
        for (int j = 0; j < n - 1 - i; j++)
            if (a[j] > a[j + 1]) { int t = a[j]; a[j] = a[j + 1]; a[j + 1] = t; }
}

/* Iterative Fibonacci */
int fib_iter(int n) {
    int a = 0, b = 1;
    while (n-- > 0) { int t = a + b; a = b; b = t; }
    return a;
}

/* Reverse a string in place */
void str_rev(char *s) {
    int i = 0, j = (int)strlen(s) - 1;
    while (i < j) { char t = s[i]; s[i++] = s[j]; s[j--] = t; }
}

/* Count vowels */
int vowels(const char *s) {
    int c = 0;
    for (; *s; s++)                          // *s is '\0' at the end → false
        if (strchr("aeiouAEIOU", *s)) c++;
    return c;
}

/* Matrix transpose (3x3, in place) */
for (int i = 0; i < 3; i++)
    for (int j = i + 1; j < 3; j++) { int t = m[i][j]; m[i][j] = m[j][i]; m[j][i] = t; }

/* Right-angled star triangle: row i prints i stars */
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i; j++) printf("*");
    printf("\n");
}
```

Loop-count shortcuts: triangle pattern prints `1 + 2 + … + n = n(n+1)/2` items. Bubble sort does about `n(n-1)/2` comparisons. Binary search takes about `log2(n)` steps.

---

## Appendix C. Linked List Operations

```c
/* Insert at end */
void push_back(struct Node **head, int v) {
    struct Node *n = create_node(v);
    if (n == NULL) return;
    if (*head == NULL) { *head = n; return; }      // empty list special case
    struct Node *cur = *head;
    while (cur->next != NULL) cur = cur->next;     // stop at LAST node
    cur->next = n;
}

/* Search */
struct Node *find(struct Node *head, int v) {
    for (; head != NULL; head = head->next)
        if (head->data == v) return head;
    return NULL;
}

/* Delete first node containing v (pointer-to-pointer avoids head special case) */
void delete_value(struct Node **head, int v) {
    while (*head != NULL && (*head)->data != v)
        head = &(*head)->next;
    if (*head != NULL) {
        struct Node *dead = *head;
        *head = dead->next;                        // unlink
        free(dead);
    }
}

/* Reverse: three pointers prev, cur, next */
struct Node *reverse_list(struct Node *head) {
    struct Node *prev = NULL, *cur = head;
    while (cur != NULL) {
        struct Node *next = cur->next;             // save
        cur->next = prev;                          // flip link
        prev = cur;                                // advance
        cur = next;
    }
    return prev;                                   // new head
}

/* Free the whole list: save next BEFORE freeing */
void free_list(struct Node *head) {
    while (head != NULL) {
        struct Node *next = head->next;
        free(head);
        head = next;
    }
}
```

Common list bugs: dereferencing `NULL` at the end of the list, losing the rest of the list by overwriting `next` before saving it, forgetting the empty-list case, using `free(cur)` and then `cur->next`, and forgetting that a function must take `struct Node **` to change `head`.
