# 📚 NPTEL — Introduction to Programming in C
### Week 3 Exam Notes | Prof. Satyadev Nandakumar, IIT Kanpur

> **Topics Covered:** `char` & ASCII · Operator Associativity · Operator Precedence · Expression Evaluation & Comma Operator · Functions (Intro, Stack, Call-by-Value, Side Effects, Forward Declarations)

---

## Topic 1: The `char` Data Type 📅 Week 3

### 1. Concept Summary
`char` stores a **single character** in 1 byte (8 bits). Its core trick: to the programmer it looks like a character, but to the machine it **is an integer** — specifically, its ASCII value. This duality lets you do arithmetic on characters, compare them, and print them as either a symbol or a number. Mastering `char` is essential for any text-processing question on NPTEL.

### 2. Key Syntax / Rules Box

```c
char ch;            // declaration
ch = 'A';           // assign using SINGLE quotes
char ch = 'a';      // initialize at declaration
char ch = 65;       // same as 'A' — integer assignment is valid
printf("%c", ch);   // prints the character: A
printf("%d", ch);   // prints the ASCII value: 65
scanf("%c", &ch);   // reads ONE character (first char of input only)
scanf("%d", &n);    // reads digits, converts to integer value
```

**Rules & Edge Cases:**
- Single quotes `'A'` → character constant. Double quotes `"A"` → string literal (different type!).
- `char ch = 65;` and `char ch = 'A';` are **equivalent** — both store the same bit pattern.
- `%c` prints the character; `%d` prints its ASCII integer.
- `scanf("%c", &ch)` on input `"12"` stores `'1'` (ASCII 49), **not** the integer 12.
- `char` is 1 byte → values 0–127 (standard ASCII) or 0–255 (extended).
- Non-printable characters (ASCII 0–31) need escape sequences.

**Escape Sequences:**
| Escape | Name | ASCII |
|--------|------|-------|
| `\n` | Newline | 10 |
| `\t` | Tab | 9 |
| `\a` | Bell (beep) | 7 |
| `\b` | Backspace | 8 |
| `\v` | Vertical Tab | 11 |
| `\xHH` | Any char (hex) | e.g. `\x41` = `'A'` |

### 3. Detailed Code Example

```c
#include <stdio.h>

int main() {
    char ch = 'A';

    // %c prints the character symbol
    printf("Character: %c\n", ch);     // Output: Character: A

    // %d prints the underlying ASCII integer
    printf("ASCII val: %d\n", ch);     // Output: ASCII val: 65

    // Integer assigned directly — perfectly valid
    char ch2 = 65;
    printf("ch2: %c\n", ch2);          // Output: ch2: A

    // Printing non-printable character via hex escape
    printf("Bell: \x7\n");             // causes a beep sound

    // char arithmetic — works because char IS an int
    char next = ch + 1;                // 65 + 1 = 66 = 'B'
    printf("Next: %c\n", next);        // Output: Next: B

    return 0;
}
```

**What would NPTEL ask about this?**

❓ What does `printf("%d", 'A');` print?
✅ **65**
💡 `'A'` is a character constant whose value equals its ASCII code. `%d` prints the integer, not the symbol.

---

❓ What is printed?
```c
char c = 'a';
c = c - 32;
printf("%c", c);
```
✅ **A**
💡 `'a'` is ASCII 97, `'A'` is ASCII 65. Difference is 32. `97 - 32 = 65 = 'A'`. Lowercase → uppercase by subtracting 32.

---

❓ `scanf("%c", &ch);` is called with input `"12"`. What is stored in `ch`?
✅ The character `'1'` (ASCII value **49**)
💡 `%c` reads exactly ONE character — the first one. It does NOT convert "12" to the integer 12.

---

### 4. Common Pitfalls Table

| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `char ch = "A";` | Compile error — `"A"` is a string, not a char | `char ch = 'A';` |
| `printf("%c", 65);` | Works but confusing — prints `A` | Fine, but use `'A'` for clarity |
| Using `%d` expecting `'0'` = 0 | `'0'` is ASCII 48, not 0 | Distinguish char `'0'` from int `0` |
| `char ch = getchar();` | May lose `EOF` (-1) since `char` can't hold -1 | `int ch = getchar();` |

### 5. Quick Recall
- `char` = 1 byte = integer = ASCII value
- `'A'` = 65, `'a'` = 97, `'0'` = 48
- `%c` → symbol, `%d` → ASCII number
- Single quotes for char constants; double quotes for strings
- `\xHH` prints any ASCII character by hex code

---

## Topic 2: ASCII Table — Abstract Properties 📅 Week 3

### 1. Concept Summary
You do **not** need to memorize the full ASCII table. What matters are the **structural properties**: digits, uppercase, and lowercase each form a **contiguous block** in the table. This lets you range-check and do case conversion using only `'A'`, `'Z'`, `'a'`, `'z'`, `'0'`, `'9'` — no magic numbers needed. The golden rule: lowercase letters appear **after** uppercase letters.

### 2. Key Syntax / Rules Box

```c
// ASCII structure (decimal values):
// Non-printable : 0–31
// Space         : 32
// Digits '0'–'9': 48–57   (contiguous)
// Uppercase A–Z : 65–90   (contiguous)
// Lowercase a–z : 97–122  (contiguous)
// Difference between any lowercase and its uppercase = 32
// 'a' - 'A' = 32  |  'b' - 'B' = 32  |  etc.

// Range checks (no memorization needed):
ch >= 'A' && ch <= 'Z'   // is uppercase
ch >= 'a' && ch <= 'z'   // is lowercase
ch >= '0' && ch <= '9'   // is digit
```

**Rules & Edge Cases:**
- Lowercase > Uppercase in ASCII — `'a' > 'A'` is **true**.
- All three blocks (digits, upper, lower) are internally consecutive.
- `'A' - 'a'` = -32 (negative! uppercase comes first numerically).
- Comparing `ch >= '0'` compares to ASCII 48, **not** the number 0.

### 3. Detailed Code Example

```c
#include <stdio.h>

int main() {
    /* --- Print the full uppercase alphabet using char arithmetic --- */
    char ch;
    for (ch = 'A'; ch <= 'Z'; ch++) {   // ch starts at 65, loops to 90
        printf("%c ", ch);               // prints A B C ... Z
    }
    printf("\n");

    /* --- Case conversion: lowercase to uppercase --- */
    char letter = 'g';
    if (letter >= 'a' && letter <= 'z') {        // confirm it's lowercase
        letter = letter + ('A' - 'a');           // add (-32) to shift up
        // 'A' - 'a' = 65 - 97 = -32
        // 'g' (103) + (-32) = 71 = 'G'
    }
    printf("Uppercase: %c\n", letter);  // Output: G

    /* --- Digit check: '5' vs 5 --- */
    char c = '5';
    if (c >= '0' && c <= '9') {
        int digit_val = c - '0';        // convert char digit to int: '5'-'0'=5
        printf("Digit value: %d\n", digit_val);  // Output: 5
    }

    return 0;
}
```

**What would NPTEL ask about this?**

❓ What does `'a' - 'A'` evaluate to?
✅ **32**
💡 `'a'` = 97, `'A'` = 65, difference = 32. This constant offset works for ALL letter pairs.

---

❓ Is `'a' > 'Z'` true or false?
✅ **True**
💡 All lowercase letters (97+) come AFTER all uppercase letters (65–90) in ASCII.

---

❓ What is the output?
```c
char ch = '5';
printf("%d", ch - '0');
```
✅ **5**
💡 `'5'` = ASCII 53, `'0'` = ASCII 48. `53 - 48 = 5`. This is the standard way to convert a digit character to its integer value.

---

### 4. Common Pitfalls Table

| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `ch > 0 && ch < 9` to check digit | Compares to integers 0 and 9, not char digits | `ch >= '0' && ch <= '9'` |
| `ch + 32` always gives lowercase | Fails if `ch` is already lowercase or not a letter | Check `ch >= 'A' && ch <= 'Z'` first |
| `1 < ch < 5` for range check | Always true in C (evaluated as `(1<ch) < 5`) | `ch > 1 && ch < 5` |

### 5. Quick Recall
- Digits, uppercase, lowercase = 3 separate contiguous blocks
- Lowercase > Uppercase in ASCII (by 32)
- `'0'` ≠ `0` — char `'0'` = integer 48
- `c - '0'` converts digit char to its integer value
- `c + ('A' - 'a')` → lowercase to uppercase

---

## Topic 3: Operator Associativity 📅 Week 3

### 1. Concept Summary
**Associativity** resolves ambiguity when the **same precedence** operators appear consecutively. It answers: left-to-right or right-to-left? Most arithmetic operators group left-to-right (math convention). The big exceptions: **assignment** (`=`) and **unary operators** are right-to-left. Getting this wrong causes chain-assignment bugs.

### 2. Key Syntax / Rules Box

```c
// LEFT-to-RIGHT associativity:
a + b + c    → (a + b) + c
10 - 5 - 15  → (10 - 5) - 15  = -10   (NOT 10 - (5-15) = 20)
a * b / c    → (a * b) / c
a < b < c    → (a < b) < c    ← TRAP: always evaluates to 0 or 1 first!

// RIGHT-to-LEFT associativity:
a = b = c = 0   → a = (b = (c = 0))   // all become 0
! - x           → !(-(x))              // unary operators chain right-to-left

// Assignment returns the assigned value:
int a, b;
a = b = 10;   // b=10 first (returns 10), then a=10
```

**Rules:**
- **Left-associative:** `+`, `-`, `*`, `/`, `%`, `<`, `>`, `<=`, `>=`, `==`, `!=`, `&&`, `||`
- **Right-associative:** `=`, `+=`, `-=`, `*=` (all assignment), unary `-`, `!`, `&`, `*`, `++`, `--`
- Assignment operator **returns the assigned value** — this enables chaining.
- Chained assignments `a = b = c = 0` are **not** evaluated left-to-right.

### 3. Detailed Code Example

```c
#include <stdio.h>

int main() {
    int a, b, c;

    /* --- Chained assignment: RIGHT-to-LEFT --- */
    a = b = c = 5;
    // Step 1: c = 5  (returns 5)
    // Step 2: b = 5  (returns 5)
    // Step 3: a = 5
    printf("%d %d %d\n", a, b, c);   // Output: 5 5 5

    /* --- Left-to-right subtraction: order matters! --- */
    int result = 10 - 5 - 3;
    // Left assoc: (10 - 5) - 3 = 5 - 3 = 2
    // NOT: 10 - (5 - 3) = 8
    printf("%d\n", result);           // Output: 2

    /* --- TRAP: chained comparison --- */
    int x = 2;
    int test = 1 < x < 5;    // WRONG for range check!
    // (1 < 2) → 1, then (1 < 5) → 1. Always 1 regardless of x!
    printf("trap: %d\n", test);       // Output: 1  (even if x = 100)

    /* --- Correct range check --- */
    int correct = (1 < x) && (x < 5);
    printf("correct: %d\n", correct); // Output: 1

    return 0;
}
```

**What would NPTEL ask about this?**

❓ What does `a = b = c = 0` do if `a`, `b`, `c` were garbage values before?
✅ Sets all three to **0** (right-to-left evaluation).
💡 `c=0` runs first, returns 0; `b=0` next, returns 0; `a=0` last.

---

❓ What is `10 - 5 - 15`?
✅ **-10**
💡 Left associativity: `(10 - 5) - 15 = 5 - 15 = -10`. Right-to-left would give `10 - (5-15) = 20` — wrong!

---

❓ Is `1 < x < 5` a valid range check in C?
✅ **No** — it always evaluates to 1 (true) for any `x`.
💡 `(1 < x)` gives 0 or 1. Both 0 and 1 are less than 5, so result is always true.

---

### 4. Common Pitfalls Table

| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `0 = a;` (LHS is not a variable) | Compile error — `0` is not an L-value | `a = 0;` |
| `a = b = c` with uninitialized `c` | Assigns undefined garbage from `c` | Initialize `c` first |
| Assuming `a - b - c` = `a - (b - c)` | Wrong: left-assoc gives `(a-b)-c` | Use parentheses if you mean `a - (b-c)` |

### 5. Quick Recall
- Associativity = tie-breaker for **same-level** operators
- Most binary operators: **left-to-right**
- Assignment `=` and unary ops: **right-to-left**
- `a = b = 0` → right-to-left, both become 0
- `1 < a < 5` is a **trap** — never use for range checks

---

## Topic 4: Operator Precedence 📅 Week 3

### 1. Concept Summary
**Precedence** decides which operator "wins" when different operators compete. Think of it as operator priority levels. Higher precedence = evaluated first. The key hierarchy to memorize for NPTEL: parentheses → unary → `* / %` → `+ -` → relational → `&&` → `||` → assignment. Parentheses always override everything.

### 2. Key Syntax / Rules Box

```c
// Precedence hierarchy (high → low):
// 1. ()           parentheses             [override all]
// 2. ! - ++ --    unary operators         [right-to-left]
// 3. * / %        multiplicative          [left-to-right]
// 4. + -          additive                [left-to-right]
// 5. < > <= >=    relational              [left-to-right]
// 6. == !=        equality                [left-to-right]
// 7. &&           logical AND             [left-to-right]
// 8. ||           logical OR              [left-to-right]
// 9. = += -= etc. assignment              [right-to-left]
// 10. ,           comma operator          [LOWEST, left-to-right]

// Classic example:
a = 10 + 5 * 4 % 2
// Step 1: 5 * 4 = 20     (higher precedence)
// Step 2: 20 % 2 = 0     (same level, left-to-right)
// Step 3: 10 + 0 = 10    (next level)
// Step 4: a = 10         (assignment last)
```

**Rules & Edge Cases:**
- `*`, `/`, `%` are the SAME level — resolved by left-to-right associativity.
- `+`, `-` are the SAME level — resolved by left-to-right associativity.
- Relational operators have **lower** precedence than arithmetic → calculations happen before comparisons.
- Assignment has **lowest** precedence (except comma) → entire RHS computed first.
- `&&` has higher precedence than `||` (AND before OR, like math).

### 3. Detailed Code Example

```c
#include <stdio.h>

int main() {
    int a, b = 2;

    /* --- Precedence walkthrough --- */
    a = 10 + 5 * 4 % 2;
    // 5*4=20, 20%2=0, 10+0=10, a=10
    printf("a = %d\n", a);       // Output: a = 10

    /* --- Assignment vs comparison precedence --- */
    a = b > 1;
    // '>' has higher prec than '='
    // b > 1 → 2 > 1 → 1 (true)
    // then a = 1
    printf("a = %d\n", a);       // Output: a = 1

    /* --- Forcing different order with parentheses --- */
    a = (b > 1);                  // same as above: a = 1
    int c = (a = b) > 1;          // (a=b) runs first → a=2, then 2>1 → c=1
    printf("a=%d, c=%d\n", a, c); // Output: a=2, c=1

    /* --- Complex expression --- */
    int x = 3, y = 2, z = 1;
    int result = x + y - z * x % y / z;
    // Step 1: z*x = 1*3 = 3
    // Step 2: 3%y = 3%2 = 1
    // Step 3: 1/z = 1/1 = 1
    // Step 4: x+y = 3+2 = 5
    // Step 5: 5 - 1 = 4
    printf("result = %d\n", result);  // Output: result = 4

    return 0;
}
```

**What would NPTEL ask about this?**

❓ What is the value of `a` after `a = 10 + 5 * 4 % 2`?
✅ **10**
💡 `*` and `%` before `+`: `5*4=20`, `20%2=0`, `10+0=10`.

---

❓ What does `a = b > 1` assign to `a` when `b = 5`?
✅ **1** (not 5)
💡 `>` has higher precedence than `=`. `b > 1` is `true` = 1. Then `a = 1`.

---

❓ Does `a + b > c` check if `(a+b) > c` or `a + (b > c)`?
✅ **(a+b) > c** — arithmetic before relational.
💡 `+` has higher precedence than `>`.

---

### 4. Common Pitfalls Table

| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `a = b > 1` expecting `a = b` | `>` runs first; `a` gets 0 or 1 | `(a = b) > 1` or just `a = b;` |
| Assuming `*` and `+` are same level | `*` runs before `+` always | Know the hierarchy |
| `!a > 0` expecting `!(a > 0)` | `!a` runs first (unary), then `> 0` | `!(a > 0)` with explicit parentheses |

### 5. Quick Recall
- Parentheses override everything
- `* / %` > `+ -` > relational > `&&` > `||` > assignment
- Arithmetic before comparison — always
- `=` has near-lowest precedence; RHS fully evaluated first
- When in doubt: **add parentheses**

---

## Topic 5: Expression Evaluation & the Comma Operator 📅 Week 3

### 1. Concept Summary
This topic covers three key ideas: (1) **short-circuit evaluation** in `&&` and `||`, (2) **L-values** (what can appear on the left of `=`), and (3) the **comma operator** — the lowest-precedence operator in C, which evaluates left-then-right and returns the rightmost value. The `1 < a < 5` trap is a classic NPTEL question.

### 2. Key Syntax / Rules Box

```c
/* --- Short-circuit evaluation --- */
// && : if LEFT is false (0), RIGHT is NOT evaluated
if (ptr != NULL && *ptr > 0) { }  // safe: *ptr only checked if ptr != NULL
// || : if LEFT is true (non-zero), RIGHT is NOT evaluated
if (x == 0 || y / x > 2) { }     // safe: division only if x != 0

/* --- L-value requirement --- */
// Left side of = must be a modifiable memory location (a variable)
a = 5;          // valid: a is an L-value
(a + b) = 5;    // INVALID: (a+b) is not an L-value → compile error

/* --- Comma operator --- */
// Evaluates left, DISCARDS result, evaluates right, RETURNS right's value
int x = (a++, b++);   // a++ runs, result discarded; b++ runs; x = value of b++

// Classic use: for loop with multiple init/update
for (sum = 0, i = 0; i < N; i++, sum += i) { }
//    ^^^^^^^^^^ comma operator in init      ^^^^^^^^^^ in update
```

**Rules:**
- Comma operator has the **LOWEST** precedence of all C operators.
- Comma as **operator** (sequences expressions) vs comma as **separator** (in `int a, b;` or function args) — context determines which.
- `&&` and `||` are **guaranteed** to short-circuit (unlike function arguments!).
- The left side of `=` must be an **L-value** — a named variable or dereferenced pointer.

### 3. Detailed Code Example

```c
#include <stdio.h>

int main() {
    int a = 1, b = 2, c = 3;

    /* --- Short-circuit: && stops at first false --- */
    int x = 10;
    // If x == 0, the second condition is never evaluated (no div-by-zero)
    if (x != 0 && 100 / x > 5) {
        printf("Safe divide\n");   // Output: Safe divide
    }

    /* --- 1 < a < 5 TRAP --- */
    // In math: means 1 < a AND a < 5
    // In C: left-assoc: (1 < a) < 5
    //   Step 1: (1 < 2) = 1 (true)
    //   Step 2: (1 < 5) = 1 (always true!)
    int val = 2;
    if (1 < val < 5) {
        printf("trap fires for val=2\n"); // fires
    }
    val = 100;  // change to 100
    if (1 < val < 5) {
        printf("trap STILL fires for val=100!\n"); // STILL fires - BUG!
    }
    // CORRECT range check:
    if (1 < val && val < 5) {
        printf("correct: this won't fire for val=100\n"); // won't print
    }

    /* --- Comma operator --- */
    int i, sum;
    // Init: sum=0 first, then i=0
    // Update: i++, then sum += i (sum gets new i each time)
    for (sum = 0, i = 1; i <= 3; i++, sum += i) { }
    printf("sum=%d, i=%d\n", sum, i); // sum=2+3+4=9, i=4

    /* --- Comma as operator vs separator --- */
    int p = 0, q = 0;
    int r = (p = 5, q = p + 1); // operator: p=5 discarded, q=6 returned
    printf("p=%d q=%d r=%d\n", p, q, r); // p=5 q=6 r=6

    return 0;
}
```

**What would NPTEL ask about this?**

❓ What is the value of `x` after `int x = (a = 3, b = a + 1, b * 2);` with `a=0, b=0`?
✅ **8**
💡 Comma evaluates left-to-right, returns rightmost: `a=3` (discard), `b=4` (discard), `b*2=8` (returned).

---

❓ Can `(a + b) = c;` appear in C code?
✅ **No** — compile error.
💡 `(a+b)` evaluates to a temporary value with no memory address. Only variables (L-values) can appear on the left of `=`.

---

❓ In `if (ptr == NULL || ptr->val > 0)`, is `ptr->val` always evaluated?
✅ **No** — if `ptr == NULL`, short-circuit stops; `ptr->val` is never evaluated (avoiding a crash).
💡 `||` short-circuits: if left is true, right is skipped.

---

### 4. Common Pitfalls Table

| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `1 < a < 5` for range check | Always true (result is 0 or 1, both < 5) | `a > 1 && a < 5` |
| `b % c - a = a + 1` | Compile error: LHS is not L-value | Separate into `b%c-a` and `a+1` statements |
| Confusing `,` in `int a, b;` with comma operator | Separator, not operator — no sequencing | They look identical; context decides |
| Expecting both sides of `&&` to always run | Short-circuit may skip right side | Don't put critical side effects on right side of `&&`/`||` |

### 5. Quick Recall
- Comma operator: left-to-right, returns **rightmost** value, **lowest** precedence
- Short-circuit: `&&` stops at first false; `||` stops at first true
- `1 < a < 5` is a **bug** — use `1 < a && a < 5`
- L-value = modifiable memory location = variable
- Comma as separator (declarations, function args) ≠ comma as operator

---

## Topic 6: Functions — Declaration, Definition & Execution 📅 Week 3

### 1. Concept Summary
Functions enable **modular programming**: solve sub-problems independently, reuse code, avoid duplication. Every function has a **declaration** (prototype — tells the compiler the interface) and a **definition** (the actual code). Parameters in the definition are **formal**; values passed at call time are **actual**. C uses **call-by-value** exclusively: the function gets a *copy* of each argument.

### 2. Key Syntax / Rules Box

```c
// DECLARATION (prototype) — must specify each parameter's type separately
int iscoprime(int a, int b);   // correct
int iscoprime(int a, b);       // WRONG — b needs its own type

// DEFINITION
int iscoprime(int a, int b) {
    // a and b are FORMAL parameters (local copies)
    // ...
    return 1;  // return exits the function immediately
}

// CALL — actual parameters
int result = iscoprime(9, 4);  // 9 and 4 are actual parameters

// Call-by-value: changes to formal params do NOT affect actual params
void swap(int a, int b) {
    int t = a; a = b; b = t;   // modifies LOCAL copies only
}                               // original variables in caller UNCHANGED

// Structure of a C program:
// 1. #include headers
// 2. Function declarations (prototypes)
// 3. Function definitions
// 4. main()
```

**Rules:**
- Each parameter in a declaration MUST have its own type: `int a, int b` NOT `int a, b`.
- `return expr;` sends the value back AND terminates the function immediately.
- Local variables and parameters are **deallocated** when function returns.
- Variables with the same name in different functions are **completely independent** (different scopes).
- C is **always call-by-value** — functions receive copies, never originals.

### 3. Detailed Code Example

```c
#include <stdio.h>

// DECLARATION (forward declaration — needed before use)
int iscoprime(int a, int b);

// DEFINITION: uses Euclidean GCD algorithm
int iscoprime(int a, int b) {
    int t;
    // Ensure a >= b for the algorithm
    if (a < b) {
        t = a; a = b; b = t;   // swap if needed
    }
    // Euclidean algorithm: GCD(a, b) = GCD(b, a%b)
    while (b != 0) {
        t = b;
        b = a % b;
        a = t;
    }
    // After loop, 'a' holds the GCD
    if (a == 1) return 1;    // GCD=1 means coprime; return exits immediately
    else return 0;
}

// Demonstrates call-by-value — swap does NOTHING to caller's variables
void swap(int a, int b) {
    int t = a;
    a = b;
    b = t;
    // a and b are LOCAL copies — caller's variables unchanged
}

int main() {
    int x = 9, y = 4;
    printf("coprime(9,4) = %d\n", iscoprime(x, y));  // Output: 1 (yes)
    printf("coprime(4,6) = %d\n", iscoprime(4, 6));   // Output: 0 (no; GCD=2)

    // Call-by-value demo
    int p = 10, q = 20;
    swap(p, q);
    printf("p=%d q=%d\n", p, q);  // Output: p=10 q=20 — UNCHANGED!

    return 0;
}
```

**What would NPTEL ask about this?**

❓ After calling `swap(p, q)` as defined above, what are the values of `p` and `q`?
✅ **Unchanged** — `p` and `q` still hold their original values.
💡 Call-by-value: `swap` receives copies. Swapping copies doesn't affect originals.

---

❓ Is `int iscoprime(int a, b);` a valid function declaration?
✅ **No** — compile error.
💡 Each parameter must have its own type. Correct: `int iscoprime(int a, int b);`

---

❓ If a function is declared as `int f()` but contains `return;` (no value), what happens?
✅ **Undefined behavior** — the caller receives an unpredictable value.
💡 Always return a value of the declared type.

---

### 4. Common Pitfalls Table

| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `int f(int a, b)` | Compile error: `b` has no type | `int f(int a, int b)` |
| Expecting `swap(a,b)` to swap originals | Call-by-value; copies are swapped | Use pointers for true swap |
| Ignoring that `return` exits immediately | Code after `return` is dead code | Structure conditionals so return is the last statement |
| Same variable name in caller and function | They're different variables in different scopes | No fix needed — just understand scope |

### 5. Quick Recall
- Declaration = prototype = interface (no body, ends with `;`)
- Definition = actual implementation
- Formal parameters = placeholders in definition; actual parameters = values passed
- `return value;` sends result AND exits function
- C = always call-by-value (copies, not originals)
- Same-named variables in different functions = **different, unrelated** variables

---

## Topic 7: The Function Call Stack 📅 Week 3

### 1. Concept Summary
Every function call gets its own **stack frame** — a dedicated block of memory on the **call stack** (LIFO). The frame holds: copies of arguments, local variables, return address (where to resume in the caller), and space for the return value. When the function returns, the frame is **destroyed**. This explains why local variables disappear after a function returns and why recursion works.

### 2. Key Syntax / Rules Box

```c
// What happens when f(x, y) is called:
// 1. Save return address (next line in caller)
// 2. Reserve space for return value
// 3. COPY actual args → formal params (call-by-value!)
// 4. Jump to function code
// 5. Allocate stack frame (local vars + params + return addr + ret val)
// 6. Execute function body
// 7. copy return value out
// 8. POP (destroy) stack frame
// 9. Jump to saved return address
// 10. Caller receives the return value

// Stack frame contents:
// [ return address ]
// [ return value   ]
// [ formal param 1 ]
// [ formal param 2 ]
// [ local var 1    ]  ← ALL ERASED when function returns
// [ local var 2    ]
```

### 3. Detailed Code Example

```c
#include <stdio.h>

int fact(int r) {
    // Stack frame: r, i, ans, return_addr, return_val
    int i, ans = 1;
    for (i = 1; i <= r; i++) {
        ans *= i;
    }
    return ans;   // return value copied out, frame erased
}

int nchoosek(int n, int k) {
    // Stack frame: n, k, t1, t2, t3, return_addr, return_val
    int t1, t2, t3;

    t1 = fact(n);       // call 1: new frame for fact(n), erased on return
    t2 = fact(k);       // call 2: new frame for fact(k), erased on return
    t3 = fact(n - k);   // call 3: new frame for fact(n-k), erased on return

    return t1 / (t2 * t3);  // frame erased on return to main
}

int main() {
    int n = 4, k = 2;
    int result = nchoosek(n, k);
    // n=4, k=2: 4!/(2!*2!) = 24/(2*2) = 6
    printf("C(%d,%d) = %d\n", n, k, result);  // Output: C(4,2) = 6
    return 0;
}
```

**What would NPTEL ask about this?**

❓ After `fact(4)` returns, can you access the local variable `ans` from inside `fact`?
✅ **No** — the stack frame is destroyed on return; `ans` no longer exists.
💡 Local variables have **automatic storage duration** — they live only during the function call.

---

❓ In `nchoosek`, after the first call to `fact(n)`, what happens to `fact`'s local variables?
✅ They are **erased** (stack frame popped).
💡 Each call creates a fresh frame. The frames for the three `fact` calls don't coexist — they're created and destroyed one at a time.

---

❓ What does "call-by-value" mean in terms of the stack?
✅ The actual argument's **value is copied** into the stack frame's parameter slot. The original variable is untouched.
💡 The stack frame contains a copy, not a reference. This is the physical mechanism behind call-by-value.

---

### 4. Common Pitfalls Table

| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Returning address of a local variable | Dangling pointer — frame destroyed | Return the value, not its address |
| Thinking function frames persist | They're destroyed on return | Use `static` or global if persistence needed |
| Assuming stack is infinite | Deep recursion causes stack overflow | Use iterative solutions for deep recursion |

### 5. Quick Recall
- Stack = LIFO memory for function calls
- Each call → new **stack frame** pushed; return → frame **popped/destroyed**
- Frame contains: return address, return value space, params, locals
- Local variables cease to exist after function returns
- Call-by-value physically implemented via copying into the stack frame

---

## Topic 8: Side Effects & Undefined Argument Evaluation Order 📅 Week 3

### 1. Concept Summary
A **side effect** changes program state beyond producing a value — e.g., assignments, I/O. **Pure expressions** only produce a value without state changes. The critical trap: C **does not guarantee** the order in which function arguments are evaluated. If arguments have side effects, the outcome is **compiler-dependent** and non-portable. Fix: perform side effects explicitly **before** the function call.

### 2. Key Syntax / Rules Box

```c
// Pure expression (no state change):
a - b * c / d     // just computes; no variable is modified

// Expression with side effect:
a = a + 1         // modifies 'a' — has a side effect

// THE TRAP: undefined argument evaluation order
// C standard says: arguments are evaluated before the call,
// but the ORDER of evaluation is UNSPECIFIED (compiler decides)
int result = minus(a = b + 1, b = a + 1);  // UNDEFINED BEHAVIOR!
// Compiler may evaluate left-to-right OR right-to-left — both valid!

// SAFE VERSION: do side effects BEFORE the call
a = b + 1;         // explicit, sequential
b = a + 1;         // now b uses the updated a
int result = minus(a, b);  // no side effects in args — safe!
```

**Rules:**
- **Pure expressions:** only compute a value; no variable changes.
- **Side-effecting expressions:** change program state (assignments, `++`, `--`, `scanf`, etc.).
- C **guarantees** argument evaluation happens before the call, but **not the order** among arguments.
- `&&` and `||` ARE guaranteed left-to-right (special case).
- Ignoring a function's return value is **valid** — common when function is called for side effects (e.g., `scanf`).

### 3. Detailed Code Example

```c
#include <stdio.h>

int minus(int a, int b) {
    return b - a;  // returns b - a
}

int main() {
    int a = 1, b = 1;

    /* --- DANGER: side effects in function arguments --- */
    // int result = minus(a = b + 1, b = a + 1);
    // Compiler A (left-to-right):  a=2, b=3 → minus(2,3) = 1
    // Compiler B (right-to-left):  b=2, a=3 → minus(3,2) = -1
    // BOTH are valid! Result is unpredictable.

    /* --- SAFE version: side effects BEFORE call --- */
    a = 1; b = 1;  // reset
    a = b + 1;     // a = 2 (b was 1)
    b = a + 1;     // b = 3 (a is now 2)
    int result = minus(a, b);  // minus(2, 3) = 1, deterministic!
    printf("result = %d\n", result);  // Output: result = 1

    /* --- Ignoring return value is legal --- */
    // scanf is called primarily for its side effect (reading input)
    // Its return value (items read) is often ignored
    // scanf("%d", &a);  // return value (1 or EOF) usually ignored

    /* --- Variable scope demo: same name, different function --- */
    // int a in main and int a in minus are DIFFERENT variables
    // They exist in different stack frames

    return 0;
}
```

**What would NPTEL ask about this?**

❓ With `a=1, b=1`, what is the output of `printf("%d", minus(a = b+1, b = a+1));`?
✅ **Undefined / compiler-dependent** (could be 1 or -1)
💡 C does not specify evaluation order of function arguments. This is a famous NPTEL trap — the correct answer is "undefined behavior."

---

❓ Is it valid to call a function and ignore its return value?
✅ **Yes** — e.g., `scanf(...)` is often called ignoring its return value.
💡 When a function is called for its **side effects** (reading input, printing), ignoring the return value is legitimate.

---

❓ Is `a = 1` a pure expression?
✅ **No** — it modifies the state of `a`. It has a side effect.
💡 Pure = only produces a value, no state change. `a = 1` changes `a` → side effect.

---

### 4. Common Pitfalls Table

| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Side effects in function args | Undefined/non-portable behavior | Pre-compute and store in variables first |
| `return;` in an `int` function | Caller gets garbage return value | Always `return value;` with the right type |
| Assuming left-to-right arg evaluation | Wrong on some compilers | Never rely on arg evaluation order |

### 5. Quick Recall
- Pure = only produces a value; side-effecting = changes state
- Assignment, `++`, `--`, I/O = side effects
- Arg evaluation order in function calls = **undefined** in C
- Fix: compute side effects **before** the function call
- `&&` and `||` short-circuit: left-to-right guaranteed (special case)

---

## Topic 9: Forward Declarations & `getchar()` / `feof()` 📅 Week 3

### 1. Concept Summary
A **forward declaration** (prototype) tells the compiler about a function's signature before its full definition. This is required when Function A calls Function B, but B is defined *after* A in the source file. `getchar()` reads one character at a time from stdin and returns `int` (not `char`) so it can represent `EOF` (-1), which doesn't fit in a `char`. `feof(stdin)` checks if the end-of-file condition has been set.

### 2. Key Syntax / Rules Box

```c
// Forward declaration syntax:
int read_next_line();     // declares before defining — tells compiler the signature

// getchar() — returns int, NOT char!
int ch;                   // MUST be int to correctly handle EOF
ch = getchar();           // reads one character; returns EOF (-1) at end-of-input
if (ch == EOF) { ... }   // EOF is typically -1 (defined in stdio.h)

// WRONG:
char ch = getchar();      // char may not hold -1 correctly → can't detect EOF

// feof() — checks if EOF indicator is set
while (!feof(stdin)) {    // keep looping until end of input
    // read next line
}

// Typical pattern to read line char-by-char:
while ((ch = getchar()) != EOF && ch != '\n') {
    // process ch
}
```

**Rules:**
- `getchar()` returns `int` — always declare the receiving variable as `int`.
- `EOF` is typically `-1` (defined in `<stdio.h>`).
- A `char` variable might not hold `-1` correctly if `char` is unsigned on the platform.
- Forward declarations end with `;` (no body).
- Function that is defined **before** it's called does NOT need a forward declaration.

### 3. Detailed Code Example

```c
#include <stdio.h>

// Forward declaration: read_next_line is defined AFTER read_all_lines
// Without this, compiler would error when read_all_lines calls it
int read_next_line();

// Defined FIRST (calls read_next_line, so needs its forward declaration)
int read_all_lines() {
    int line_count = 0;
    while (!feof(stdin)) {         // loop until EOF (Ctrl-D on Linux)
        if (read_next_line()) {    // returns 1 if valid line, 0 if blank/EOF
            line_count++;
        }
    }
    return line_count;
}

// Defined SECOND (the actual implementation)
int read_next_line() {
    int ch;       // MUST be int — not char — to detect EOF (-1)
    int count = 0;

    // Read chars until newline or EOF
    while ((ch = getchar()) != EOF && ch != '\n') {
        count++;  // count non-newline, non-EOF chars
    }

    // Returns 1 (true) if line had ≥1 real character; 0 for blank lines
    return count > 0;   // expression evaluates to 1 or 0
}

int main() {
    int total = read_all_lines();
    printf("Total lines: %d\n", total);
    return 0;
}
```

**What would NPTEL ask about this?**

❓ Why does `getchar()` return `int` instead of `char`?
✅ To correctly represent `EOF` (typically -1), which cannot be stored in a `char`.
💡 `char` ranges 0–127 (or 0–255 unsigned). `-1` doesn't fit. Using `int ch` lets the program distinguish EOF from valid characters.

---

❓ What is a forward declaration and when is it needed?
✅ A function prototype placed before the function's full definition. Needed when Function A calls Function B but B is **defined after** A in the source file.
💡 Without it, the compiler doesn't know B's return type/parameters when compiling A → compile error.

---

❓ What does `return count > 0;` return from `read_next_line`?
✅ `1` if `count > 0` is true; `0` if false.
💡 Relational expressions in C evaluate to `int` 0 or 1. This is a clean idiom for returning a boolean flag from an `int` function.

---

### 4. Common Pitfalls Table

| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `char ch = getchar();` | May fail to detect EOF on some platforms | `int ch = getchar();` |
| Omitting forward declaration | Compile error when function called before defined | Add prototype before caller |
| `while (feof(stdin))` | Reads AFTER EOF; misses last line | `while (!feof(stdin))` |
| Blank line counted as a line | Depends on definition of "line" | Check `count > 0` to exclude blank lines |

### 5. Quick Recall
- Forward declaration = prototype = function signature + `;` (no body)
- `getchar()` returns **`int`** — always use `int ch`
- `EOF` = typically **-1**; can't be stored in `char` reliably
- `feof(stdin)` = true after Ctrl-D (Linux) or Ctrl-Z (Windows)
- `return count > 0;` = returns 1 or 0 (idiomatic boolean return)

---

## 📊 Master Operator Precedence & Associativity Table

| Level | Operators | Associativity |
|-------|-----------|---------------|
| 1 (highest) | `()` parentheses | — |
| 2 | `!` `-`(unary) `++` `--` `&`(addr) `*`(deref) | Right-to-Left |
| 3 | `*` `/` `%` | Left-to-Right |
| 4 | `+` `-` | Left-to-Right |
| 5 | `<` `>` `<=` `>=` | Left-to-Right |
| 6 | `==` `!=` | Left-to-Right |
| 7 | `&&` | Left-to-Right |
| 8 | `\|\|` | Left-to-Right |
| 9 | `=` `+=` `-=` `*=` etc. | Right-to-Left |
| 10 (lowest) | `,` (comma operator) | Left-to-Right |

---

## 🚀 Key ASCII Values to Remember

| Character | ASCII (Dec) | Hex |
|-----------|-------------|-----|
| `'0'` | 48 | 0x30 |
| `'9'` | 57 | 0x39 |
| `'A'` | 65 | 0x41 |
| `'Z'` | 90 | 0x5A |
| `'a'` | 97 | 0x61 |
| `'z'` | 122 | 0x7A |
| Space | 32 | 0x20 |
| Newline `\n` | 10 | 0x0A |
| `'\0'` (null) | 0 | 0x00 |
| `EOF` | -1 | — |

**Key offset:** `'a' - 'A' = 32` (applies to all letter pairs)

---

## ⚡ Exam-Day Quick Reference

- `char` = integer = ASCII value; `%c` prints symbol, `%d` prints number
- `'0'` ≠ `0` — char digit 0 is ASCII 48
- `1 < a < 5` is a **BUG** — use `a > 1 && a < 5`
- Associativity = tie-breaker for same-precedence operators
- Assignment `=` is right-to-left; almost everything else is left-to-right
- `*` `/` `%` beat `+` `-` always (BODMAS)
- Comma operator: lowest precedence, evaluates left→right, returns rightmost value
- Function args: evaluated before call but in **undefined order** — never put side effects in args
- Call-by-value: functions get **copies** — caller's variables unchanged
- `getchar()` returns **`int`** — use `int ch`, not `char ch`
- Forward declaration needed when function called before its definition in file
- Stack frame = temporary memory per function call, destroyed on return

---

## 🧪 Weekly Assignment Analysis — Assignment 3

---

### Question 1 — Factorial of a Number

> **Task:** Complete `int findfactorial(int k)` to return `k!` (product of all positive integers from 1 to k). Read N numbers and print factorial of each.

---

#### ✅ Correct Solution (Cleaned)

```c
#include <stdio.h>

/* Function: computes k! iteratively */
int findfactorial(int k) {
    int p = 1;                  // p holds the running product; start at 1 (not 0!)
    for (int i = 1; i <= k; i++) {
        p *= i;                 // multiply p by each number from 1 to k
    }
    return p;                   // return the final product = k!
}

int main() {
    int n, k;
    scanf("%d", &n);            // read how many numbers follow

    for (int i = 0; i < n; i++) {
        scanf("%d", &k);        // read each number
        printf("%d ", findfactorial(k));  // print its factorial
    }

    return 0;
}
```

#### 🔍 Line-by-Line Explanation

| Line / Part | What it does | Why it matters |
|-------------|-------------|----------------|
| `int p = 1;` | Initializes running product to **1** | Must be 1, not 0 — multiplying by 0 gives 0 always |
| `for (int i = 1; i <= k; i++)` | Loop from 1 up to and **including** k | `<=` is critical — `< k` would miss the last factor |
| `p *= i;` | Shorthand for `p = p * i` | Builds factorial step-by-step: 1×1×2×3×…×k |
| `return p;` | Sends result back to caller | Call-by-value — caller gets the computed value |
| `scanf("%d", &n)` then loop | Reads count first, then each ki | Standard multi-input NPTEL pattern |
| `printf("%d ", findfactorial(k))` | Calls function inline in printf | Return value used directly as an argument |

#### 🔁 Dry Run: `findfactorial(4)`

| Iteration | `i` | `p = p * i` | `p` |
|-----------|-----|-------------|-----|
| Start | — | — | 1 |
| 1 | 1 | 1 × 1 | 1 |
| 2 | 2 | 1 × 2 | 2 |
| 3 | 3 | 2 × 3 | 6 |
| 4 | 4 | 6 × 4 | **24** |

Returns **24** ✓ (4! = 4 × 3 × 2 × 1 = 24)

#### ❓ NPTEL Traps

❓ What happens if `p` is initialized to `0` instead of `1`?
✅ `findfactorial(k)` always returns **0** for any k.
💡 `0 * anything = 0`. The product collapses. Always initialize accumulator for multiplication to **1**.

---

❓ What is the output for input `k = 1`?
✅ **1** (since 1! = 1)
💡 The loop runs once: `p = 1 * 1 = 1`. Edge case that NPTEL commonly tests.

---

❓ Would `for (int i = 1; i < k; i++)` work correctly?
✅ **No** — it would compute `(k-1)!` instead of `k!` because it misses the final multiplication by `k`.
💡 `i <= k` includes k; `i < k` stops one short. Classic off-by-one error.

---

#### ⚠️ Common Pitfalls

| Mistake | What happens | Fix |
|---------|-------------|-----|
| `int p = 0;` | Returns 0 for all inputs | `int p = 1;` |
| `i < k` instead of `i <= k` | Returns `(k-1)!` | Use `i <= k` |
| Using `int` for large factorials | Overflow for k ≥ 13 | Use `long long` for large k |
| `p = i` instead of `p *= i` | Only returns k, not k! | `p *= i` or `p = p * i` |

---

### Question 2 — Parking Fee Calculator

> **Task:** Complete `int parkingfee(int hours)` using slab-based pricing:
> - 0 hours → Rs. 0
> - 1–2 hours → Rs. 20 per hour
> - Beyond 2 hours → Rs. 40 (for first 2h) + Rs. 30 × (hours − 2)

---

#### ✅ Correct Solution (Cleaned)

```c
#include <stdio.h>

/* Function: computes parking fee based on slab rules */
int parkingfee(int hours) {
    if (hours <= 0)             // guard: 0 or negative hours → no fee
        return 0;

    if (hours <= 2)             // slab 1: up to 2 hours → Rs.20/hour
        return hours * 20;

    return 40 + (hours - 2) * 30;
    // 40 = fixed cost for first 2 hours (2 × 20)
    // (hours - 2) = extra hours beyond the first 2
    // * 30 = Rs.30 for each extra hour
}

int main() {
    int hours;
    scanf("%d", &hours);
    printf("%d", parkingfee(hours));
    return 0;
}
```

#### 🔍 Line-by-Line Explanation

| Condition | Formula | Example |
|-----------|---------|---------|
| `hours <= 0` | Return 0 | Input: 0 → Output: 0 |
| `hours <= 2` | `hours * 20` | Input: 2 → 2×20 = **40** |
| `hours > 2` | `40 + (hours-2)*30` | Input: 5 → 40 + 3×30 = **130** |

#### 🔁 Dry Run Examples

| Input (hours) | Calculation | Output (Rs.) |
|--------------|-------------|--------------|
| 0 | Return 0 | **0** |
| 1 | 1 × 20 | **20** |
| 2 | 2 × 20 | **40** |
| 3 | 40 + (1 × 30) | **70** |
| 5 | 40 + (3 × 30) | **130** |
| 10 | 40 + (8 × 30) | **280** |

#### ❓ NPTEL Traps

❓ What does the function return for `hours = 2`?
✅ **40** (hits `hours <= 2` slab: `2 * 20 = 40`)
💡 The boundary value (2) belongs to the cheaper slab. Boundary conditions are classic NPTEL traps.

---

❓ What does `return 40 + (hours - 2) * 30` compute for `hours = 5`?
✅ **130** → `40 + (5-2)*30 = 40 + 90 = 130`
💡 The `40` is pre-computed cost for the first 2 hours. `(hours-2)` is the remaining hours × Rs.30.

---

❓ What happens if the `hours <= 0` guard is removed and `hours = 0` is passed?
✅ The `hours <= 2` branch catches it: `0 * 20 = 0` — still returns 0, so functionally the same here. But the guard is good defensive programming.
💡 However for negative inputs without the guard: `(-3) * 20 = -60` — wrong. Always guard edge cases.

---

❓ What is the operator precedence in `40 + (hours - 2) * 30`?
✅ Parentheses first: `(hours - 2)`. Then `* 30`. Then `+ 40`.
💡 Without parentheses `40 + hours - 2 * 30` = `40 + hours - 60` — completely wrong result!

---

#### ⚠️ Common Pitfalls

| Mistake | What happens | Fix |
|---------|-------------|-----|
| `30 + (hours-2)*30` instead of `40 + ...` | Wrong base (first 2 hours = 2×20 = 40, not 30) | `40 + (hours-2)*30` |
| Missing guard for `hours <= 0` | Negative fee for negative input | Add `if (hours <= 0) return 0;` |
| `(hours-2)*30` without `+ 40` | Ignores cost of the first 2 hours | Must add base cost of 40 |
| Wrong slab boundary: `hours < 2` | Treats 2 hours as extra-rate | Use `hours <= 2` (2 hours is in cheap slab) |

---

### Question 3 — Caesar Cipher (Shift a Letter)

> **Task:** Given a lowercase letter and an integer `k` (0 ≤ k ≤ 25), shift the letter `k` positions forward in the alphabet. Wrap around from `'z'` back to `'a'` using modular arithmetic.

---

#### ✅ Correct Solution (Cleaned)

```c
#include <stdio.h>

int main() {
    char letter;
    int k;

    scanf(" %c", &letter);   // note the space before %c — skips leftover whitespace
    scanf("%d", &k);

    /* Caesar cipher formula:
       1. (letter - 'a')       → convert to 0-based index (a=0, b=1, ..., z=25)
       2. + k                  → shift forward by k positions
       3. % 26                 → wrap around using modulo (keeps result in 0–25)
       4. + 'a'                → convert back to ASCII character             */
    letter = ((letter - 'a' + k) % 26) + 'a';

    printf("%c", letter);

    return 0;
}
```

#### 🔍 The Caesar Cipher Formula — Step by Step

The key line is:
```c
letter = ((letter - 'a' + k) % 26) + 'a';
```

Let's trace it for `letter = 'x'`, `k = 5`:

| Step | Operation | Value | Explanation |
|------|-----------|-------|-------------|
| 1 | `letter - 'a'` | `120 - 97 = 23` | `'x'` is the 23rd letter (0-indexed) |
| 2 | `+ k` | `23 + 5 = 28` | Shift forward 5 positions |
| 3 | `% 26` | `28 % 26 = 2` | Wrap around — 28 goes past 'z', lands at index 2 |
| 4 | `+ 'a'` | `2 + 97 = 99` | Convert index back to ASCII |
| Result | `(char)99` | `'c'` | `'x'` shifted 5 → **'c'** ✓ |

#### 🔁 Dry Run Examples

| Input Letter | k | Index (`-'a'`) | After shift | After `%26` | Output |
|-------------|---|----------------|-------------|-------------|--------|
| `'a'` | 3 | 0 | 3 | 3 | `'d'` |
| `'z'` | 1 | 25 | 26 | 0 | `'a'` (wraps!) |
| `'y'` | 3 | 24 | 27 | 1 | `'b'` (wraps!) |
| `'m'` | 0 | 12 | 12 | 12 | `'m'` (no shift) |
| `'a'` | 25 | 0 | 25 | 25 | `'z'` |

#### ❓ NPTEL Traps

❓ What is the output for `letter = 'z'`, `k = 1`?
✅ `'a'`
💡 `'z' - 'a' = 25`, `25 + 1 = 26`, `26 % 26 = 0`, `0 + 'a' = 'a'`. The modulo wraps it perfectly.

---

❓ Why `% 26` and not `% 25`?
✅ There are **26** letters in the alphabet (indices 0–25). `% 26` keeps the result in range 0–25.
💡 `% 25` would be wrong — it wraps at 25 instead of 26, skipping `'z'` from being a valid wrap target.

---

❓ Why `letter - 'a'` instead of just using `letter` directly?
✅ `letter - 'a'` converts to a **0-based index** (a=0 … z=25). Without it, you'd be doing arithmetic on raw ASCII values (97–122) and `% 26` would give wrong results.
💡 For example: `'a' % 26 = 97 % 26 = 19` — wrong. `('a' - 'a') % 26 = 0` — correct.

---

❓ Why is there a space before `%c` in `scanf(" %c", &letter)`?
✅ The space skips any **leading whitespace** (including `\n` from a previous `Enter` keypress).
💡 Without the space, `scanf("%c", &letter)` might read the leftover newline character from stdin as the input, giving unexpected results.

---

❓ What is the output for `letter = 'a'`, `k = 0`?
✅ `'a'` — no shift, same letter.
💡 `(0 + 0) % 26 + 'a' = 'a'`. The formula correctly handles the no-shift case.

---

#### ⚠️ Common Pitfalls

| Mistake | What happens | Fix |
|---------|-------------|-----|
| `(letter + k) % 26 + 'a'` | Wrong — doesn't normalize to 0-based first | `((letter - 'a' + k) % 26) + 'a'` |
| `% 25` instead of `% 26` | Incorrect wrap — 'z' never reached properly | `% 26` (26 letters in alphabet) |
| Missing `+ 'a'` at the end | Returns 0–25 (index), not a character | Always add `'a'` back to re-encode |
| `scanf("%c", &letter)` without leading space | May read leftover `\n` from previous input | `scanf(" %c", &letter)` with space |
| `char k` instead of `int k` | Works for 0–25 but bad practice | Use `int k` for shift value |

---

### 📌 Assignment 3 — Concept Cross-Reference

| Question | Topics from Week 3 Lecture |
|----------|---------------------------|
| Q1 — Factorial | Functions (definition, return value), `for` loop, multiplicative accumulator, call-by-value |
| Q2 — Parking Fee | Functions, if-else branching, operator precedence (`*` before `+`), boundary conditions |
| Q3 — Caesar Cipher | `char` as integer, ASCII arithmetic, `char - 'a'` normalization, modulo `%`, `scanf(" %c")` whitespace |

### ⚡ Assignment Quick Recall
- Factorial accumulator must start at **1**, not 0; loop uses `i <= k` not `i < k`
- Parking fee base: **40** for first 2 hours (2 × 20), then **30** per extra hour
- Caesar cipher formula: `((letter - 'a' + k) % 26) + 'a'` — normalize → shift → wrap → re-encode
- Always `% 26` for alphabet wrap (26 letters), never `% 25`
- `scanf(" %c", &letter)` — the **space before `%c`** skips leftover newline in input buffer
