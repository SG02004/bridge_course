# 📘 Week 6 Notes — Multidimensional Arrays & File Handling
**Course:** Introduction to Programming in C | Prof. Satyadev Nandakumar, IIT Kanpur

---

## 📅 Week 6 — 2D Arrays: Basics

### Concept Summary
A 2D array (`type name[rows][cols]`) is C's built-in way to store a grid/matrix. Think of it as an array of arrays, laid out **row by row** in memory. You index it as `mat[i][j]` — row first, column second, both 0-based. This is the foundation for every matrix problem (symmetric check, Sudoku, tic-tac-toe) you'll see in assignments.

### Key Syntax / Rules Box
```c
double mat[5][6];          // 5 rows, 6 columns
mat[2][3] = 1.0;           // set row 2, col 3
scanf("%f", &mat[i][j]);   // reading needs &
printf("%f", mat[i][j]);   // printing does not

// Partial initialization -> rest becomes 0
int a[2][3] = { {1, 2}, {4} };   // a = {{1,2,0},{4,0,0}}

// As a function parameter: COLUMNS MUST be specified, ROWS can be omitted
void fill(double m[][6], int rows) { ... }
```
- ✅ Rule: when passing a 2D array to a function, you **must** give the column count; row count is optional.
- ✅ `%f` in `scanf` skips all leading whitespace automatically — so extra spaces/newlines in input don't break reading.
- ⚠️ Common mistake: forgetting `&` in `scanf(&mat[i][j])`, or mixing up row/column order.
- ⚠️ Un-initialized elements in partial initialization become `0`, NOT garbage.

### Detailed Code Example
```c
#include <stdio.h>

// Column count (6) is mandatory in the parameter type; rows is a separate int.
void print_matrix(double m[][6], int rows) {
    for (int i = 0; i < rows; i++) {          // outer loop = rows
        for (int j = 0; j < 6; j++) {         // inner loop = columns
            printf("%.1f ", m[i][j]);
        }
        printf("\n");
    }
}

int main() {
    double mat[3][6] = { {1,2,3,4,5,6}, {7,8}, {0} };
    print_matrix(mat, 3);
    return 0;
}
```

### What would NPTEL ask about this?
- ❓ Can you write `void f(double m[3][])`? → ✅ No, compile error → 💡 Rows can be left blank, but **columns can never be omitted** — the compiler needs the column count to compute the address of `m[i][j]`.
- ❓ What does `int a[2][3] = {{1,2},{4}};` store in `a[1][2]`? → ✅ `0` → 💡 Missing elements in an initializer are zero-filled, row by row.
- ❓ If you swap `i` and `j` in `scanf("%f", &mat[j][i])` by mistake while looping `i` over rows, `j` over columns — what happens? → ✅ Compiles fine, runs, but transposes your input silently → 💡 No runtime error occurs; this is a logic bug, a favorite NPTEL "spot the mistake" trap.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Omitting column size in function parameter | Compile-time error | `void f(int m[][N], int rows)` |
| Forgetting `&` in `scanf` for array element | Garbage/crash (undefined behavior) | `scanf("%d", &A[i][j]);` |
| Assuming uninitialized elements are garbage | Wrong prediction on exam | They are auto-zeroed in partial init |
| Row/column mixed in nested loop | Silent transpose, wrong output, no error | Keep outer loop = row, inner = column consistently |

### Quick Recall
- 2D array = `type name[rows][cols]`, access via `mat[i][j]`.
- Function params: **column count mandatory, row count optional**.
- Partial initializer → remaining elements become `0`.

---

## 📅 Week 6 — 2D Arrays & Pointers (Row-Major Form)

### Concept Summary
Internally, C stores a 2D array as **one long 1D array**, row after row — this is "row-major form." A 3×5 matrix is really 15 contiguous integers in memory. This is *why* the compiler insists on knowing the column count: it needs that number to calculate how many elements to "skip" to jump from one row to the next (`mat + 1` = skip one full row).

### Key Syntax / Rules Box
```c
int mat[3][5];
// Conceptual (matrix) view:      Row-major (actual memory) view:
// mat    -> row 0                0 1 2 3 4 | 5 6 7 8 9 | 10 11 12 13 14
// mat+1  -> row 1
// mat+2  -> row 2

mat[i][j]  ==  *(*(mat + i) + j)   // subscript is sugar for this pointer math
```
- `mat + 1` on a 2D array skips **columns-many elements** (an entire row), NOT just 1 element.
- `mat + i` skips `i * columns` elements.
- This is exactly why column count must be part of the type — it's baked into the pointer arithmetic.

### Declaration Cheat-Sheet (classic NPTEL trap — operator precedence: `[]` binds tighter than `*`)
| Declaration | Meaning | Use case |
|---|---|---|
| `int* mat` | pointer to int (1D array) | simple 1D array |
| `int* mat[5]` | **array of 5** `int*` pointers | array of arrays / ragged array |
| `int (*mat)[5]` | pointer to **an array of 5 ints** | the real type of a 2D array with 5 columns |
| `int** mat` | pointer to pointer to int | dynamically allocated / ragged 2D array |

### Detailed Code Example
```c
#include <stdio.h>

void make_identity(double m[][10], int n) {   // must fix column count = 10
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            m[i][j] = (i == j) ? 1 : 0;        // diagonal = 1, else 0
}

int main() {
    double id[10][10];
    make_identity(id, 10);   // works only for exactly 10 columns
    printf("%.0f\n", id[3][3]);  // prints 1
    return 0;
}
```

### What would NPTEL ask about this?
- ❓ Given `int (*mat)[5]`, what does `mat + 1` point to? → ✅ The start of the 2nd row (skips 5 ints) → 💡 Pointer arithmetic scales by the pointed-to type's size — here the type is "array of 5 ints."
- ❓ Which is correct: `int* mat[5]` or `int (*mat)[5]` for a fixed 2D array with 5 columns? → ✅ `int (*mat)[5]` → 💡 Parentheses force `mat` to be a pointer *first*; without them, `[]` binds first, making `mat` an array of pointers instead.
- ❓ `mat[0][0]` for `int (*mat)[5]` simplifies to what expression? → ✅ `*(*mat)` → 💡 `*(*(mat+0)+0)` → `*(*mat + 0)` → `*(*mat)`.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Treating `mat+1` as "next element" for a 2D array | Wrong address, wrong element read | Remember it skips a full row (column-count elements) |
| Confusing `int* mat[5]` with `int (*mat)[5]` | Wrong type passed to function, compiler warning/error | Add parentheses: `(*mat)` for pointer-to-array |
| Passing `mat + 1` to a function expecting `int*` | Type mismatch — `int(*)[5]` ≠ `int*` | Pass `*(mat+1)` or `mat[1]` instead (decays to `int*`) |

### Quick Recall
- C stores 2D arrays in row-major (one long contiguous block).
- `mat + i` skips `i` full rows, not `i` elements.
- `int (*mat)[N]` = correct type for a fixed-N-column 2D array; `int* mat[N]` = array of N pointers (different thing!).

---

## 📅 Week 6 — Passing Rows to 1D Functions / 2D Search

### Concept Summary
A single row of `int (*mat)[5]` **decays to `int*`** once you dereference it (`*(mat+i)` or `mat[i]`) — so you can feed it directly into any function written for 1D arrays. This is how you build 2D search/processing on top of 1D building blocks, and how you "return" more than one value (row + column) using pointer output-parameters.

### Key Syntax / Rules Box
```c
int search(int a[], int n, int key);   // 1D search: returns index or -1

// Calling search on row i of a 2D array mat (int (*mat)[5]):
search(mat + i, 5, key);     // ❌ WRONG — type mismatch: int(*)[5] vs int*
search(*(mat + i), 5, key);  // ✅ CORRECT — row decays to int*
search(mat[i], 5, key);      // ✅ CORRECT — same thing, syntactic sugar
```
- Returning multiple values: pass **pointers** as extra parameters; the function writes results into `*row`, `*col`.

### Detailed Code Example
```c
#include <stdio.h>

int search(int a[], int n, int key) {
    for (int i = 0; i < n; i++)
        if (a[i] == key) return i;   // found -> index
    return -1;                       // not found
}

// "Returns" row & col via pointers since C functions return only ONE value directly
void search2D(int (*mat)[5], int n_rows, int key, int *row, int *col) {
    *row = -1; *col = -1;            // default: not found
    for (int i = 0; i < n_rows; i++) {
        int c = search(mat[i], 5, key);  // row decays to int* here
        if (c != -1) { *row = i; *col = c; return; }  // stop at first match
    }
}

int main() {
    int mat[3][5] = {{1,2,3,4,5},{6,7,8,9,10},{11,12,13,14,15}};
    int r, c;
    search2D(mat, 3, 9, &r, &c);
    printf("Found at (%d, %d)\n", r, c);  // (1, 3)
    return 0;
}
```

### What would NPTEL ask about this?
- ❓ Why does `search(mat + 1, 5, key)` fail to compile / warn? → ✅ `mat + 1` has type `int (*)[5]`, but `search` expects `int*` → 💡 An entire row-pointer is not the same as a pointer-to-first-element; you must dereference once more.
- ❓ Why pass `int *row, int *col` instead of returning a struct or two ints? → ✅ It's the standard C idiom because a function can only `return` one value directly → 💡 Passing addresses lets the callee modify the caller's variables ("output parameters").
- ❓ What would happen if `search2D` didn't `return;` after finding a match? → ✅ It would keep looping and overwrite `*row`/`*col` with the **last** match instead of the first → 💡 Classic "missing early exit" bug in MCQ traps.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Passing `mat + i` instead of `mat[i]`/`*(mat+i)` | Type mismatch compile error | Always dereference once when passing a row to a 1D function |
| Forgetting to initialize `*row`/`*col` to -1 | Garbage value if key not found | Explicitly set defaults before the search loop |
| Not breaking/returning after first match | Later matches overwrite earlier (correct) result silently | Add `return;` or a `found` flag to stop the loop |

### Quick Recall
- `mat[i]` / `*(mat+i)` → decays to `int*`, safe to pass to 1D functions.
- `mat+i` alone → still `int(*)[N]`, NOT compatible with `int*` parameters.
- Multiple return values in C = pass pointers, write through them.

---

## 📅 Week 6 — Array of Arrays (Ragged Arrays)

### Concept Summary
Regular 2D arrays force **every row to be the same length**, wasting memory for uneven data (like strings). An "array of arrays" (`char* strings[N]`) instead stores an array of *pointers*, where each pointer can point to a row of a completely different length — a "ragged array." This is the standard trick for storing lists of strings (e.g. month names).

### Key Syntax / Rules Box
```c
char* month_names[] = {
    "January", "February", "March", "April", "May", "June",
    "July", "August", "September", "October", "November", "December"
};
// month_names is char** — array of char* pointers, each pointing to a string of its own length

month_names[i]        // -> char*, the i-th string
month_names[i][j]     // -> char, the j-th letter of the i-th string
*(*(month_names+i)+j) // same thing via pointer arithmetic
```
- ✅ `char* strings[7]` = array of 7 pointers (because `[]` binds tighter than `*`).
- ✅ Memory layout: the **array of pointers is contiguous**, but the strings they point to can be **scattered anywhere** in memory.
- ⚠️ 2D array (`char matrix[3][7]`) = fully contiguous, fixed row length, wastes space on short strings.

### Detailed Code Example
```c
#include <stdio.h>

int main() {
    char* month_names[] = {
        "January", "February", "March", "April", "May", "June",
        "July", "August", "September", "October", "November", "December"
    };

    int month_index = 9;  // September
    if (month_index >= 1 && month_index <= 12) {
        printf("%s\n", month_names[month_index - 1]);  // decays to char* for %s
    } else {
        printf("Invalid month\n");
    }

    printf("%c\n", month_names[0][0]);  // 'J' — first char of first string
    return 0;
}
```

### What would NPTEL ask about this?
- ❓ What is the type of `month_names`? → ✅ `char**` → 💡 An array of `char*` decays to a pointer-to-pointer when treated as a value.
- ❓ What does `**month_names` give you? → ✅ `'J'` (a single `char`) → 💡 One `*` gets you the first string (`char*`), a second `*` gets you its first character.
- ❓ Why is `char* movies[]` better than `char movies[N][20]` for movie titles of varying length? → ✅ It avoids wasting memory padding short titles to a fixed column width → 💡 Ragged storage: each string uses exactly the memory it needs; only the pointer array itself is fixed-size and contiguous.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Reading `char* strings[7]` as "pointer to array of 7 chars" | Wrong mental model — it's actually 7 separate pointers | Remember `[]` beats `*` in precedence: it's an *array* of pointers |
| Assuming array-of-arrays rows are contiguous in memory | Wrong pointer arithmetic assumptions between rows | Only the pointer array is contiguous; actual strings can be anywhere |
| Using `%s` on `month_names[i][j]` (a single char) | Undefined behavior / garbage output | Use `%c` for a single character, `%s` for the whole string (`month_names[i]`) |

### Quick Recall
- `char* strings[N]` = array of N pointers → enables ragged (variable-length) rows.
- Type of the whole thing = `char**`; one `*` → row (`char*`), two `*` → single char.
- Ragged arrays trade contiguous memory for flexible row lengths — ideal for strings.

---

## 📅 Week 6 — File Handling: Basics

### Concept Summary
A "file" in an OS isn't just data on disk — it's *any addressable resource* (even `/dev/null`). Every C program automatically has 3 standard streams: `stdin` (fd 0), `stdout` (fd 1), `stderr` (fd 2). Beyond these, C's `stdio.h` gives you `fopen`/`fscanf`/`fprintf`/`fclose` to manually open, read/write, and close **any** file — the same functions you already know (`scanf`, `printf`) but with an explicit `FILE*` target.

### Key Syntax / Rules Box
```c
FILE *fp = fopen("data.txt", "r");   // "r"=read, "w"=write(truncate), "a"=append
if (fp == NULL) {                    // ALWAYS check this
    fprintf(stderr, "Error opening file\n");
    return 1;
}
fscanf(fp, "%d", &x);     // like scanf, but reads from fp instead of stdin
fprintf(fp, "%d", x);     // like printf, but writes to fp instead of stdout
fclose(fp);               // release resources — don't forget this!
```
- `"r"` → file **must exist**, else `fopen` returns `NULL`.
- `"w"` → creates new file OR **truncates (wipes)** existing one.
- `"a"` → creates new file OR appends to the end of an existing one.
- Shell redirection (`<`, `>`, `2>`) is a **shell** feature, not a C feature — it just redirects the default streams before your program even starts.

### Detailed Code Example
```c
#include <stdio.h>

// Generic — doesn't open/close files itself, promotes reuse
void copy_file(FILE* fromfp, FILE* tofp) {
    char c;
    while (!feof(fromfp)) {         // loop until end-of-file
        fscanf(fromfp, "%c", &c);   // read one char from source
        fprintf(tofp, "%c", c);     // write it to destination
    }
}

int main() {
    FILE *fp1 = fopen("input.txt", "r");
    if (fp1 == NULL) {
        fprintf(stderr, "Error: could not open input.txt\n");
        return 1;
    }
    copy_file(fp1, stdout);   // stdout is itself a valid FILE*
    fclose(fp1);
    return 0;
}
```

### What would NPTEL ask about this?
- ❓ What does `fopen("x.txt", "r")` return if `x.txt` doesn't exist? → ✅ `NULL` → 💡 Read mode requires the file to already exist; always check before using the pointer.
- ❓ What's wrong with the `copy_file` loop above at true end-of-file (subtle bug)? → ✅ It can print one extra garbage/duplicate character at EOF → 💡 `feof` only becomes true *after* a failed read attempt, so the loop body executes once more than expected — a classic "off-by-one with feof" trap; better to check `fscanf`'s return value instead.
- ❓ Which mode wipes existing file content immediately upon opening? → ✅ `"w"` → 💡 `"a"` preserves content and appends; `"r"` doesn't allow writing at all.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Not checking `fopen()`'s return value | Crash (NULL pointer dereference) on later `fscanf`/`fprintf` | Always `if (fp == NULL) { ... }` before using `fp` |
| Using `"w"` when you meant to preserve old data | Existing file content silently deleted | Use `"a"` to append instead |
| Relying on `while(!feof(fp))` alone | Off-by-one: last iteration may process garbage/duplicate data | Check the return value of `fscanf`/`fread` instead (e.g., `while (fscanf(fp,"%c",&c)==1)`) |
| Forgetting `fclose()` | Resource leak, unflushed buffered data may be lost | Always `fclose(fp)` when done |

### Quick Recall
- Default streams: `stdin`(0), `stdout`(1), `stderr`(2) — redirection (`<`,`>`,`2>`) is a shell trick, not C.
- `fopen`/`fscanf`/`fprintf`/`fclose` are the file-analogs of `scanf`/`printf` — always check `fopen` for `NULL`.
- `"r"` needs existing file; `"w"` truncates/creates; `"a"` appends/creates.

---

## 📅 Week 6 — Advanced File Handling

### Concept Summary
Beyond basic read/write, C gives finer control: `feof`/`ferror` check a stream's status, `fseek`/`ftell` let you jump to and report arbitrary byte positions (non-sequential access), and the `+` modes (`r+`, `w+`, `a+`) let a single file be both read and written.

### Key Syntax / Rules Box
```c
feof(fp);     // non-zero if end-of-file indicator is set
ferror(fp);   // non-zero if an error occurred on this stream

fseek(fp, 10, SEEK_SET);   // go to byte 10 from the START
fseek(fp, 10, SEEK_CUR);   // move 10 bytes forward from CURRENT position
fseek(fp, -10, SEEK_END);  // go to 10 bytes before the END

long pos = ftell(fp);      // current byte offset from start (-1L on error)
```
| Mode | Needs file to exist? | On open | Reads from | Writes go to |
|---|---|---|---|---|
| `r+` | Yes (else `NULL`) | starts at beginning | anywhere via `fseek` | wherever pointer is (after `fseek`) |
| `w+` | No — creates/**truncates** | starts at beginning, file emptied | anywhere via `fseek` | wherever pointer is |
| `a+` | No — creates if absent | pointer at end for existing file | anywhere via `fseek` | **always at end**, ignoring `fseek` |

### Detailed Code Example
```c
#include <stdio.h>

int main() {
    FILE *fp = fopen("data.txt", "r+");
    if (fp == NULL) { fprintf(stderr, "File must exist for r+\n"); return 1; }

    long start = ftell(fp);        // remember position (0, beginning)

    fseek(fp, 5, SEEK_SET);        // jump to byte 5
    char c;
    fscanf(fp, "%c", &c);          // read the character there
    printf("Byte at pos 5: %c\n", c);

    fseek(fp, start, SEEK_SET);    // go back to where we started
    fclose(fp);
    return 0;
}
```

### What would NPTEL ask about this?
- ❓ In `a+` mode, if you `fseek` to the middle of the file and then call `fprintf`, where does the new data go? → ✅ Always appended at the **end** of the file → 💡 `a+` forces all writes to the end regardless of `fseek`; only reads respect the sought position.
- ❓ What does `fseek(fp, -10, SEEK_END)` do? → ✅ Positions the pointer 10 bytes before the end of file → 💡 `SEEK_END` measures offset backward (negative) from EOF; a positive offset here would try to go past the file, which is invalid on most systems.
- ❓ Difference between `r+` and `w+` when the file already has content? → ✅ `r+` keeps existing content; `w+` erases it immediately on open → 💡 `w+` always truncates existing files, `r+` never does (and fails if the file is missing).

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Using `w+` expecting to preserve old data | Existing content wiped instantly on `fopen` | Use `r+` (file must already exist) to preserve data |
| Expecting `fseek` to control write position in `a+` mode | Data still written at end, confusing bug | Know that `a+` writes always go to EOF, `fseek` only affects reads |
| Treating `ftell`'s -1L return as a valid position | Silent logic error later in the program | Check `ftell(fp) == -1L` for error before using the value |
| Using positive offset with `SEEK_END` | Undefined/invalid position beyond file bounds | Use negative offsets with `SEEK_END` |

### Quick Recall
- `feof`/`ferror` → check status (0 = fine/not-yet-EOF, non-zero = EOF/error).
- `fseek(fp, offset, ORIGIN)` with `SEEK_SET`/`SEEK_CUR`/`SEEK_END`; `ftell` reports current position.
- `r+`=must exist, no truncate | `w+`=creates/truncates | `a+`=writes always go to end.

---

## 🧪 Weekly Assignment Analysis — Assignment 6

### Question 1 — Check Symmetric Matrix
**Task:** Complete `int isSymmetric(int A[][n], int n)` — return 1 if `A[i][j] == A[j][i]` for all `i, j`, else 0.

**Solution:**
```c
#include <stdio.h>

int isSymmetric(int A[10][10], int n) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (A[i][j] != A[j][i]) {
                return 0;   // mismatch found -> not symmetric
            }
        }
    }
    return 1;               // no mismatch anywhere -> symmetric
}

int main() {
    int n;
    scanf("%d", &n);
    int A[10][10];
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            scanf("%d", &A[i][j]);
    printf("%d", isSymmetric(A, n));
    return 0;
}
```
**Why it works:** A matrix is symmetric exactly when every mirrored pair across the main diagonal is equal. The nested loop checks *every* `(i,j)` pair (including `i==j`, which trivially matches itself), and returns `0` the moment any mismatch is found — an early exit that avoids unnecessary work. If the loops complete without ever returning `0`, every pair matched, so it returns `1`.
**Why alternatives are wrong:** Checking only `i < j` (upper triangle) also works and is slightly more efficient, but checking `A[i][j] == A[i][j]` (same index twice) or comparing against a fixed row would never actually verify the transpose relationship — a common wrong "solution" that always evaluates true and outputs `1` even for non-symmetric matrices.
**Array note:** `A[10][10]` is used inside the function so the compiler knows the column stride (10) — matches the *"you can assume n < 10"* constraint in the problem, sidestepping the need for `A[][n]` with a runtime `n`.

---

### Question 2 — Sudoku Validator
**Task:** Validate a completed 9×9 Sudoku: every row, column, and 3×3 subgrid must contain digits 1–9 exactly once.

**Solution:**
```c
#include <stdio.h>

int main() {
    int board[9][9];
    for (int i = 0; i < 9; i++)
        for (int j = 0; j < 9; j++)
            scanf("%d", &board[i][j]);

    // 1. Check rows
    for (int i = 0; i < 9; i++) {
        int count[10] = {0};                 // count[d] tracks digit d's occurrences
        for (int j = 0; j < 9; j++) {
            int num = board[i][j];
            if (num < 1 || num > 9 || count[num] == 1) {  // out of range OR repeated
                printf("Invalid Sudoku");
                return 0;
            }
            count[num] = 1;
        }
    }

    // 2. Check columns (same idea, loop transposed)
    for (int j = 0; j < 9; j++) {
        int count[10] = {0};
        for (int i = 0; i < 9; i++) {
            int num = board[i][j];
            if (count[num] == 1) { printf("Invalid Sudoku"); return 0; }
            count[num] = 1;
        }
    }

    // 3. Check each 3x3 subgrid
    for (int r = 0; r < 9; r += 3) {          // top-left row of each block
        for (int c = 0; c < 9; c += 3) {      // top-left col of each block
            int count[10] = {0};
            for (int i = 0; i < 3; i++)
                for (int j = 0; j < 3; j++) {
                    int num = board[r + i][c + j];   // offset into the block
                    if (count[num] == 1) { printf("Invalid Sudoku"); return 0; }
                    count[num] = 1;
                }
        }
    }

    printf("Valid Sudoku");
    return 0;
}
```
**Why it works:** A `count[10]` array (frequency table for digits 0–9) is a classic pattern for "each value exactly once" checks. Each of the 3 checks (row/column/subgrid) resets a fresh `count` array and flags duplicates immediately via `count[num] == 1`. The `r += 3, c += 3` double loop is the standard trick for visiting each of the nine 3×3 blocks by their top-left corner, then a nested `i,j` (0–2) loop walks each cell within that block.
**Why range check only appears in the row-check:** Once the row-check passes for every row, every value is already guaranteed to be in `1..9` — so column/subgrid checks only need to test for repeats, not repeat the bounds check (a minor redundancy NPTEL might quiz you to spot/remove).
**Common wrong approach:** Using a single shared `count[10]` array across all rows (declared outside the loop, not reset each iteration) — this would incorrectly flag false duplicates once a digit appears in a later row, since old counts never clear.

---

### Question 3 — Tic-Tac-Toe: Find the Winner
**Task:** Complete `char findWinner(char board[3][3])` — return `'X'`, `'O'`, or `'N'` (no winner) by checking rows, columns, and both diagonals.

**Solution:**
```c
#include <stdio.h>

char findWinner(char board[3][3]) {
    /* Check rows */
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2])
            return board[i][0];              // all 3 in the row match
    }

    /* Check columns */
    for (int j = 0; j < 3; j++) {
        if (board[0][j] == board[1][j] && board[1][j] == board[2][j])
            return board[0][j];              // all 3 in the column match
    }

    /* Check main diagonal (top-left to bottom-right) */
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2])
        return board[0][0];

    /* Check secondary diagonal (top-right to bottom-left) */
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0])
        return board[0][2];

    return 'N';                              // nothing matched -> no winner
}

int main() {
    char board[3][3];
    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            scanf(" %c", &board[i][j]);      // leading space skips whitespace/newlines

    char winner = findWinner(board);
    if (winner == 'X') printf("Player X wins");
    else if (winner == 'O') printf("Player O wins");
    else printf("No winner");
    return 0;
}
```
**Why it works:** All 8 possible winning lines (3 rows, 3 columns, 2 diagonals) are checked exhaustively and independently; each check compares all three cells of that line for equality and returns the shared symbol immediately upon a match. Since a valid finished board can have at most one winner, returning as soon as *any* line matches is safe and correct.
**Why `scanf(" %c", ...)` needs the leading space:** `%c` (unlike `%d`/`%f`) does **not** skip whitespace by default — without the leading space in `" %c"`, `scanf` would read the space/newline characters between board entries as if they were board symbols, corrupting the board. This is a very common NPTEL trap question on `%c` behavior.
**Why checking board[0][0] alone (without the second `&&`) would be wrong:** Comparing only `board[0][0] == board[1][1]` isn't enough — two cells could coincidentally match while the third differs, so all winning-line checks require *both* pairwise comparisons (`a==b && b==c`) to confirm all three cells are identical.
