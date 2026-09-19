# 📘 Week 6 Notes — Multidimensional Arrays & File Handling
**Course:** Introduction to Programming in C | Prof. Satyadev Nandakumar, IIT Kanpur

---

## 📅 Week 6 — 2D Arrays: Basics

### Concept Summary
A 2D array (`type name[rows][cols]`) is C's built-in way to store a grid or matrix, and it is best understood as an array whose every element is itself an array (a row). You reach a single cell with `mat[i][j]`: `i` picks the row, `j` picks the column, and both start at 0. Because C has to work out where `mat[i][j]` lives in memory, the compiler needs to know how wide a row is. That is why, when you pass a 2D array to a function, the column count must appear in the parameter type, while the row count can be left blank (or passed separately as an `int`). Partial initializers are zero-filled rather than left as garbage, which makes it easy to declare a mostly-empty matrix. Everything later in this week (symmetric check, Sudoku, tic-tac-toe) is just nested loops over this structure, with the outer loop on rows and the inner loop on columns.

### Key Syntax / Rules Box
```c
double mat[5][6];          // 5 rows, 6 columns
mat[2][3] = 1.0;           // set row 2, col 3
scanf("%lf", &mat[i][j]);  // reading needs & (and %lf for double)
printf("%f", mat[i][j]);   // printing does not need &

// Partial initialization -> rest becomes 0
int a[2][3] = { {1, 2}, {4} };   // a = {{1,2,0},{4,0,0}}

// As a function parameter: COLUMNS MUST be specified, ROWS can be omitted
void fill(double m[][6], int rows) { ... }
```
- ✅ Rule: when passing a 2D array to a function, you **must** give the column count; row count is optional.
- ✅ `%f`/`%lf`/`%d` in `scanf` skip all leading whitespace automatically — so extra spaces/newlines in input don't break reading.
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
- ❓ If you swap `i` and `j` in `scanf("%lf", &mat[j][i])` by mistake while looping `i` over rows, `j` over columns — what happens? → ✅ Compiles fine, runs, but transposes your input silently → 💡 No runtime error occurs; this is a logic bug, a favorite NPTEL "spot the mistake" trap.

### Quick Recall
- 2D array = `type name[rows][cols]`, access via `mat[i][j]`.
- Function params: **column count mandatory, row count optional**.
- Partial initializer → remaining elements become `0`.

---

## 📅 Week 6 — 2D Arrays & Pointers (Row-Major Form)

### Concept Summary
Although we draw a 2D array as a grid, memory is just one long line of cells, so C stores the rows one after another in a single contiguous block. This is called row-major form: a 3×5 matrix is really 15 ints in a row, with row 1 starting right after row 0 ends. Once you see it this way, the column-count rule from the previous section makes sense. To find `mat[i][j]`, the compiler jumps `i` whole rows (each `columns` elements long) and then `j` more elements, so it cannot do the arithmetic without knowing the row width. The same logic explains why `mat + 1` moves to the start of the *next row* rather than the next element: pointer arithmetic always scales by the size of the thing being pointed to, and here that thing is an entire row. Subscripts like `mat[i][j]` are simply shorthand for this pointer arithmetic.

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

### Quick Recall
- C stores 2D arrays in row-major (one long contiguous block).
- `mat + i` skips `i` full rows, not `i` elements.
- `int (*mat)[N]` = correct type for a fixed-N-column 2D array; `int* mat[N]` = array of N pointers (different thing!).

---

## 📅 Week 6 — Passing Rows to 1D Functions / 2D Search

### Concept Summary
Good code reuses small pieces, and a 2D array is just a stack of 1D arrays, so you can process each row with a function you already wrote for 1D arrays. The catch is types: `mat + i` has type "pointer to a row" (`int (*)[5]`), which is not the same as `int*`, so passing it to a 1D function fails. Dereferencing once (`*(mat + i)`, or equivalently `mat[i]`) gives you the row itself, which decays to a plain `int*` pointing at its first element, and that fits a 1D function perfectly. The second idea here is returning more than one value. A C function can only `return` one thing, so to report both a row and a column you pass in the addresses of two variables and let the function write the results through those pointers. Defaulting those outputs to -1 first gives you a clean "not found" signal.

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

### Quick Recall
- `mat[i]` / `*(mat+i)` → decays to `int*`, safe to pass to 1D functions.
- `mat+i` alone → still `int(*)[N]`, NOT compatible with `int*` parameters.
- Multiple return values in C = pass pointers, write through them.

---

## 📅 Week 6 — Array of Arrays (Ragged Arrays)

### Concept Summary
A regular 2D array forces every row to be exactly the same length, which is wasteful when your data is uneven, such as a list of names or month titles. If you store them in `char names[12][10]`, short words like "May" still occupy the full 10 columns. The alternative is an array of pointers, `char* names[12]`, where each element is just a pointer and each pointer can aim at a string of any length. This is called a ragged array. Only the array of pointers is guaranteed to be contiguous; the strings they point to can sit anywhere in memory, so you can't do row-skipping pointer arithmetic across them like you can with a true 2D array. The trade-off is flexibility and saved space in exchange for a less regular memory layout. The parsing trick to remember is precedence: `[]` binds tighter than `*`, so `char* strings[7]` reads as "array of 7 pointers to char."

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

### Quick Recall
- `char* strings[N]` = array of N pointers → enables ragged (variable-length) rows.
- Type of the whole thing = `char**`; one `*` → row (`char*`), two `*` → single char.
- Ragged arrays trade contiguous memory for flexible row lengths — ideal for strings.

---

## 📅 Week 6 — File Handling: Basics

### Concept Summary
To an operating system, a "file" is any resource you can read from or write to, not just a document on disk. Every C program starts with three of these already open: `stdin` (fd 0), `stdout` (fd 1), and `stderr` (fd 2), which is what `scanf`, `printf`, and error messages use behind the scenes. To work with any other file you use the same idea with an explicit target: `fopen` opens it and gives you a `FILE*` handle, `fscanf`/`fprintf` behave like `scanf`/`printf` but use that handle, and `fclose` releases it. The open mode decides what happens on the way in: `"r"` demands an existing file, `"w"` creates or wipes, and `"a"` creates or appends. `fopen` returns `NULL` when it fails, so you always check it before using the handle, otherwise the next read or write crashes. Shell redirection (`<`, `>`, `2>`) is not part of C at all; the shell simply rewires the three standard streams before your program starts.

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
- ❓ What's wrong with the `copy_file` loop above at true end-of-file (subtle bug)? → ✅ It can print one extra garbage/duplicate character at EOF → 💡 `feof` only becomes true *after* a failed read attempt, so the loop body executes once more than expected — a classic "off-by-one with feof" trap; better to check `fscanf`'s return value instead (e.g., `while (fscanf(fp,"%c",&c)==1)`).
- ❓ Which mode wipes existing file content immediately upon opening? → ✅ `"w"` → 💡 `"a"` preserves content and appends; `"r"` doesn't allow writing at all.

### Quick Recall
- Default streams: `stdin`(0), `stdout`(1), `stderr`(2) — redirection (`<`,`>`,`2>`) is a shell trick, not C.
- `fopen`/`fscanf`/`fprintf`/`fclose` are the file-analogs of `scanf`/`printf` — always check `fopen` for `NULL`, and always `fclose` when done.
- `"r"` needs existing file; `"w"` truncates/creates; `"a"` appends/creates.

---

## 📅 Week 6 — Advanced File Handling

### Concept Summary
Basic file handling reads a file from start to finish, but real programs often need to jump around or both read and write the same file. C tracks a current position inside every open file, and `fseek` moves that position (from the start, the current spot, or the end) while `ftell` reports it as a byte offset. This gives you non-sequential access without re-reading everything. The `+` modes extend the basic ones so a single handle can do both reading and writing, and they differ only in how the file is treated on open. `r+` keeps the contents and needs the file to exist, `w+` creates the file or wipes it, and `a+` creates or keeps it but forces every write to the end, no matter where you `fseek`. `feof` and `ferror` round things out by letting you check whether a stream hit the end or hit an error.

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

### Quick Recall
- `feof`/`ferror` → check status (0 = fine/not-yet-EOF, non-zero = EOF/error).
- `fseek(fp, offset, ORIGIN)` with `SEEK_SET`/`SEEK_CUR`/`SEEK_END`; `ftell` reports current position (check for `-1L`).
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
