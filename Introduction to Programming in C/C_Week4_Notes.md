# 📘 Introduction to Programming in C — Week 4 Notes
**Course:** IIT Kanpur (Prof. Satyadev Nandakumar) | **Exam:** MCQ/MSQ, code-heavy
**Topics:** Program tracing, Arrays, Strings, Pointers, Pointer Arithmetic, Functions with Pointers, `sizeof`, Dynamic Memory (`malloc`/`free`)

---

## 1. Program Tracing & Basic Structure 📅 Week 4

### Concept Summary
Every C program starts execution at `main()`. Statements run top-to-bottom, each ending in `;`, with `{}` marking blocks. `#include <stdio.h>` pulls in library functions like `printf`. Comments (`/* */` or `//`) are ignored by the compiler but vital for readability. `\n` is a **single** special character (not two) that moves output to a new line.

### Key Syntax / Rules Box
```c
#include <stdio.h>   // preprocessor directive - gives access to printf

int main() {          // entry point of every C program
    printf("Hi\n");   // statement ends in ; ; \n = ONE newline character
    return 0;          // ends main
}
```
- `\n` is ONE character (escape sequence), NOT two — don't confuse with `\` vs `/`.
- `printf` does **not** auto-add a newline — multiple `printf`s without `\n` print on the same line.
- Comments never affect logic/output — NPTEL loves hiding comments around real code to test if you skip them correctly.
- `//` single-line comments work in modern C compilers (GCC), though lecture emphasizes `/* */`.
- 256 total characters in C (2⁸), including special/control characters.

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    printf("welcome to");     // no \n -> next printf continues on same line
    printf("C programming\n"); // \n moves cursor to next line after printing
    return 0;
}
// Output: welcome toC programming
```

**What would NPTEL ask about this?**
- ❓ `printf("A");printf("B\n");printf("C");` → output?
  ✅ `AB\nC` (i.e., "AB" then newline then "C")
  💡 No `\n` between A and B means they concatenate on one line; `\n` after B forces a break before C.
- ❓ Does `/* printf("X"); */ printf("Y");` print anything besides Y?
  ✅ No — only "Y" prints.
  💡 Anything inside `/* ... */` is invisible to the compiler, even valid code.
- ❓ How many characters does `\n` count as in memory?
  ✅ 1 character.
  💡 It's an *escape sequence* representing a single newline byte, despite being typed as two symbols.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Forgetting `;` | Compilation error | Add `;` after every statement |
| Using `/` instead of `\` for `\n` | Compiler error / wrong token | Use `\n` (backslash) |
| Assuming `printf` auto-newlines | Output runs together unexpectedly | Add `\n` explicitly where needed |

### Quick Recall
- Execution starts at `main`; sequential, semicolon-terminated statements.
- `\n` = one character; comments are compiler-invisible.

---

## 2. Array Declaration & Initialization 📅 Week 4

### Concept Summary
Arrays store same-type elements contiguously in memory, indexed from 0. In ANSI C, array size must be a **constant expression** (VLAs from user input aren't standard). Initializer lists can set values at declaration; unspecified trailing elements auto-become **0** — never left as junk **only if at least one initializer is given**.

### Key Syntax / Rules Box
```c
int num[10];                              // uninitialized -> junk values
int num[] = {-2, 3, 5, -7, 1, 11, 12};    // size = 7 (implicit, from list count)
int num[10] = {-2, 3, 5, -7, 1, 11, 12};  // size 10, rest (num[7..9]) = 0
int num[6] = {-2,3,5,-7,1,11,12};         // ❌ COMPILE ERROR: too many initializers
float w[10*10];                            // OK: constant expression allowed
int size; scanf("%d",&size);
float w[size];                             // ❌ VLA — not standard ANSI C
```
- Fully uninitialized array = **junk values** (undefined garbage), NOT zero.
- Partial initializer list → remaining elements = **0** (guaranteed).
- More initializers than declared size → **compile-time error**.
- Initializer values can be constant expressions: `'A'` → ASCII 65, `7*25*1023+'1'` all evaluated at compile time.
- Float value assigned to `int` array truncates (e.g., `25.25` → `25`).
- Variable expressions (e.g. `curr*curr+5`) in initializer lists are **non-standard** — may work on GCC but not portable.

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int num[10] = {-2, 3, 5, -7, 1, 11, 12}; // only 7 given
    for (int i = 0; i < 10; i++)
        printf("%d ", num[i]); // last 3 auto-zeroed
    return 0;
}
// Output: -2 3 5 -7 1 11 12 0 0 0
```

**What would NPTEL ask about this?**
- ❓ `int a[5] = {1,2};` → value of `a[4]`?
  ✅ `0`
  💡 Partial init guarantees remaining elements are zero-filled, not junk.
- ❓ `int a[3] = {1,2,3,4};` → compiles?
  ✅ No, compile error.
  💡 More initializers than declared size is illegal in C.
- ❓ `int a[100]; printf("%d", a[50]);` → output?
  ✅ Undefined/garbage (junk value) — cannot be predicted.
  💡 No initializer list at all means no guarantee of zeroing.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Declaring `int a[n]` with `n` from `scanf` | Non-portable VLA, may not compile on all compilers | Use a constant or `#define` for size |
| Assuming uninitialized array = 0 | Junk/garbage values | Explicitly initialize, even partially |
| Overfilling initializer list | Compile error | Match list size ≤ declared size |

### Quick Recall
- 0-based indexing; partial init → rest = 0; full omission → junk; too many initializers = error.

---

## 3. Character Arrays & Strings 📅 Week 4

### Concept Summary
A C "string" is just a `char` array terminated by the **null character `\0`**. String constants (`"..."`) auto-append `\0`; manual char-by-char init needs it explicitly. `printf("%s", ...)` prints until it hits the **first** `\0` — characters after that are still in memory but invisible to string functions.

### Key Syntax / Rules Box
```c
char s[] = {'I',' ','a','m',' ','D','O','N','\0'}; // manual: '\0' required!
char s2[] = "IamDON";                                // auto-adds '\0'
printf("%s", s2);                                     // prints until \0
```
- `%s` stops at the **first** `\0` it finds — not the array's declared size.
- Inserting `\0` mid-array truncates `%s` output there; remaining chars still exist (recoverable with `putchar` loop).
- Space character must still be in single quotes: `' '`.
- `%s` requires a `char*`/char array — passing a raw non-string char array without `\0` is undefined behavior.

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    char str[] = "IamGR8DON";   // 'I','a','m','G','R','8','D','O','N','\0'
    str[4] = '\0';              // manually insert null at index 4 (was 'R')
    printf("%s\n", str);        // stops at str[4]
    for (int i = 0; i < 10; i++) // full array still has 10 slots (incl. orig \0)
        putchar(str[i]);        // prints ALL chars, ignoring embedded \0 visually
    return 0;
}
// printf output: IamG
// putchar loop prints: IamG (then invisible \0) 8DON (then invisible \0)
```

**What would NPTEL ask about this?**
- ❓ `char s[]="Hello"; s[2]='\0'; printf("%s",s);` → output?
  ✅ `He`
  💡 `%s` truncates at the first `\0`, regardless of what follows.
- ❓ Does data after an inserted `\0` get deleted from memory?
  ✅ No — it's untouched, just unreachable via `%s`.
  💡 Only string functions honor `\0`; raw memory is unaffected.
- ❓ `char s[]={'a','b','c'};` (no `\0`) then `printf("%s",s);` → behavior?
  ✅ Undefined behavior (keeps printing garbage until it randomly finds a `\0` in memory).
  💡 Missing null terminator is a classic NPTEL "spot the bug" trap.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Manual char array without `'\0'` | UB with `%s`/string functions | Always add `'\0'` as last element |
| Assuming `%s` prints full array size | Prints only up to first `\0` | Track logical string length separately if needed |
| Forgetting space needs quotes | Compile error | `' '` not just a bare space |

### Quick Recall
- String = char array + `\0`; `%s` stops at first `\0`; string literals auto-terminate.

---

## 4. Pointers: Basics & Array Relationship 📅 Week 4

### Concept Summary
A pointer is a variable that stores a **memory address**. `&x` gets the address of `x`; `*ptr` dereferences (reads/writes the value `ptr` points to). Crucially, an **array name decays to a pointer** to its first element (`num` ≈ address of `num[0]`), linking arrays and pointers tightly.

### Key Syntax / Rules Box
```c
int a;
int *ptr;        // declares ptr as "pointer to int"
ptr = &a;         // ptr now holds address of a
*ptr = 10;        // sets a = 10 (via dereference)
int num[10];
// 'num' itself behaves like &num[0]
scanf("%d", ptr);           // no & needed — ptr IS already an address
scanf("%d", &num[1]);       // & needed for plain array element
```
- `&` and `*` are inverse operations.
- Pointer arithmetic supports `+`/`-` (scaled, see Topic 5) and relational comparisons (`==`,`!=`,`<`,`>` etc.); **NOT** `*`, `/`, `%`.
- `*ptr = *ptr + 5;` is valid — `*ptr` acts exactly like the variable it points to, on both sides of `=`.
- `scanf` always needs an address as its 2nd+ argument — that's why `&` is required for plain variables but not for pointers/array names.

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int num[10];
    int *ptr;
    ptr = &num[1];      // ptr points to num[1]
    scanf("%d", ptr);   // stores input directly into num[1], no & needed
    *ptr = *ptr + 5;     // read num[1], add 5, write back to num[1]
    printf("%d\n", num[1]); // prints (input+5)
    return 0;
}
```

**What would NPTEL ask about this?**
- ❓ `int a=5, *p=&a; *p=*p+5; printf("%d",a);` → output?
  ✅ `10`
  💡 `*p` is an alias for `a`; both sides of `=` operate on the same memory.
- ❓ Is `int *ptr; *ptr = 5;` (without assigning `ptr` an address first) safe?
  ✅ No — undefined behavior (dereferencing an uninitialized/wild pointer).
  💡 A declared-but-unassigned pointer holds a garbage address.
- ❓ Can you do `ptr1 * ptr2` for two int pointers?
  ✅ No — illegal; multiplication isn't defined for pointers.
  💡 Only `+`, `-` (with integers) and relational comparisons are valid pointer ops.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Dereferencing uninitialized pointer | UB, likely crash | Always assign `ptr = &var;` before `*ptr` |
| Adding `&` before a pointer in `scanf` | Wrong address passed (address-of-pointer) | Pass pointer directly: `scanf("%d", ptr);` |
| Confusing `num` (array) with `num[0]` (value) | Type mismatch errors | `num` = address; `num[0]` = value at that address |

### Quick Recall
- Pointer = address holder; `&`=get address, `*`=get/set value; array name decays to pointer to element 0.

---

## 5. Pointer Arithmetic 📅 Week 4

### Concept Summary
`ptr + i` doesn't add `i` bytes — it adds `i * sizeof(type)` bytes, moving to the *i-th next element* of that type. This is why `array[i]` is defined as exactly `*(array + i)`. Arithmetic is only **well-defined within array bounds** (or one-past-the-end for comparison); going further is undefined behavior.

### Key Syntax / Rules Box
```c
int num[] = {10, 22, 60, -1, 5};
*(num + 1);      // == num[1] == 22  (scaled by sizeof(int))
char str[] = "hello world";
char *p = str + 6;  // moves 6 BYTES (char is 1 byte) -> points to 'w'
printf("%s", p);     // prints "world"
printf("%s", p - 5); // moves back -> prints from str[1]
```
- **Array-Pointer Equivalence:** `array[i]` ⟺ `*(array + i)` — literally how the compiler translates it.
- Weird trivia: `f[i] == i[f]` (both = `*(f+i)`) — never write this, but NPTEL may test recognition.
- Valid pointer arithmetic range: `array` to `array + n` (n = size) — `array + n` is valid for comparison ONLY, not for dereferencing. `array + n+1` or `array - 1` = undefined behavior.
- Relational comparisons (`<`,`>`) only well-defined for pointers into the **same array**; `==`/`!=` valid for same-type pointers generally.

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int num[] = {10, 22, 60, -1, 5};
    printf("%d %d %d\n", *(num+1), *(num+2), *(num+3)); // 22 60 -1
    char str[] = "BANTI is a nice girl";
    char *ptr = str + 6;      // points to str[6] = 'i'
    printf("%s\n", ptr);      // "is a nice girl"
    printf("%s\n", ptr - 5);  // back to str[1] -> "ANTI is a nice girl"
    return 0;
}
```

**What would NPTEL ask about this?**
- ❓ `int a[10]; a+10` — is dereferencing `*(a+10)` legal?
  ✅ No — `a+10` (one-past-end) is valid to *compute/compare* but dereferencing it is UB.
  💡 Valid indices are 0..9; index 10 is out of bounds even though the address itself is "allowed to exist."
- ❓ Given `char s[]="ABCDE";` what does `*(s+2)` evaluate to?
  ✅ `'C'`
  💡 `char` pointer arithmetic moves 1 byte per step = same as index.
- ❓ Is `f[i]` legal to write as `i[f]`?
  ✅ Yes, technically compiles and works (commutative addition), but bad practice.
  💡 Tests recognition of `*(a+b) == *(b+a)` — a classic "surprising but valid" NPTEL trap.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Assuming `ptr+1` always adds 1 byte | Wrong for non-char types | Remember scaling by `sizeof(type)` |
| Dereferencing `array+n` (one past end) | Undefined behavior | Only compare against it, never dereference |
| Comparing pointers from *different* arrays with `<`/`>` | Undefined behavior | Only relationally compare pointers within the same array |

### Quick Recall
- `ptr + i` = `ptr + i*sizeof(type)`; `array[i]` ≡ `*(array+i)`; never dereference outside bounds.

---

## 6. Functions with Pointer Arguments — The `swap` Problem 📅 Week 4

### Concept Summary
C is strictly **call-by-value** — functions get *copies* of arguments, so a naive `swap(int x, int y)` cannot affect the caller's variables. The fix: pass **addresses** (`&a`, `&b`) into pointer parameters, then dereference inside the function to modify the original memory.

### Key Syntax / Rules Box
```c
void swap(int *ptra, int *ptrb) {
    int temp = *ptra;
    *ptra = *ptrb;
    *ptrb = temp;
}
// call: swap(&a, &b);
```
- Even with pointers, C is still call-by-value — it's the **address** (a value) that gets copied into `ptra`/`ptrb`, not the variable itself.
- Swapping the pointers themselves (`ptra = ptrb;`) inside the function does **nothing** to the caller — only swapping `*ptra`/`*ptrb` (the pointed-to values) works.
- `void` return type = function performs an action, doesn't compute a return value.

### Detailed Code Example
```c
#include <stdio.h>
void swap(int *ptra, int *ptrb) {
    int temp;
    temp = *ptra;   // save value pointed to by ptra
    *ptra = *ptrb;  // overwrite a's slot with b's value
    *ptrb = temp;   // overwrite b's slot with saved a value
}
int main() {
    int a = 1, b = 2;
    swap(&a, &b);               // pass ADDRESSES
    printf("%d %d\n", a, b);    // 2 1 -- originals changed!
    return 0;
}
```

**What would NPTEL ask about this?**
- ❓ `void swap(int x, int y){int t=x;x=y;y=t;}` called as `swap(a,b);` — does `a`,`b` change in `main`?
  ✅ No — call-by-value copies only; changes are local to `x`,`y`.
  💡 Classic "spot the bug" — missing pointers means no real swap.
- ❓ 
```c
void badswap(int *pa,int *pb){int *t=pa;pa=pb;pb=t;}
badswap(&a,&b);
```
does this swap `a` and `b`?
  ✅ No — it swaps the local pointer copies `pa`/`pb`, not the values `*pa`/`*pb`.
  💡 Swapping pointers ≠ swapping pointed-to data; a very common NPTEL trap.
- ❓ Why does `swap(&a,&b)` still count as "call by value" in C?
  ✅ Because the *address values* `&a`,`&b` are copied into `ptra`,`ptrb`.
  💡 C has no true "call by reference" — pointers simulate it via copied addresses.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `swap(int x, int y)` without pointers | Originals unchanged | Use `int *x, int *y` + dereference |
| Swapping pointer variables instead of values | No effect on caller | Swap `*ptra`/`*ptrb`, not `ptra`/`ptrb` |
| Forgetting `&` at call site | Type mismatch / compile error | `swap(&a, &b);` |

### Quick Recall
- Call-by-value always; pass addresses + dereference to modify caller's data; swapping pointers ≠ swapping values.

---

## 7. Pointer Arithmetic for Subarray Copy 📅 Week 4

### Concept Summary
A function written for "copy from index 0" can be **reused for any subarray** by passing shifted base addresses (`from + i`, `to + j`) instead of writing a new function. This works because the callee treats whatever address it receives as "index 0" of its own view.

### Key Syntax / Rules Box
```c
int copy_array(int a[], int b[], int n) {
    for (int i = 0; i < n; i++) b[i] = a[i];
    return 0;
}
int copy_array_2(int from[], int i, int to[], int j, int n) {
    copy_array(from + i, to + j, n); // shift base addresses, reuse logic
    return 0;
}
```
- `copy_array` is "unaware" it received a shifted address — it just treats its parameter as array index 0.
- `(f + 2)[1]` == `*((f+2)+1)` == `*(f+3)` == `f[3]` — chained pointer-index arithmetic.
- This trick relies entirely on **array-pointer equivalence**.

### Detailed Code Example
```c
#include <stdio.h>
int copy_array(int a[], int b[], int n) {
    for (int k = 0; k < n; k++) b[k] = a[k]; // a[k] == from[i+k] when shifted
    return 0;
}
int copy_array_2(int from[], int i, int to[], int j, int n) {
    copy_array(from + i, to + j, n); // from[i]->to[j], from[i+1]->to[j+1]...
    return 0;
}
int main() {
    int f[] = {0,1,2,3,4,5,6}, t[10] = {0};
    copy_array_2(f, 2, t, 4, 3); // copies f[2..4] into t[4..6]
    for (int k=0;k<10;k++) printf("%d ", t[k]);
    return 0;
}
// Output: 0 0 0 0 2 3 4 0 0 0
```

**What would NPTEL ask about this?**
- ❓ `copy_array_2(f, 2, t, 4, 5)` — which element ends up at `t[4]`?
  ✅ `f[2]`
  💡 Base shift means `to[j+k] = from[i+k]`; at `k=0`, `t[4]=f[2]`.
- ❓ Is `f[3]` equivalent to `(f+2)[1]`?
  ✅ Yes.
  💡 Both reduce to `*(f+3)`.
- ❓ Does `copy_array` need modification to support subarrays?
  ✅ No — reused as-is via pointer shifting.
  💡 The whole point of the lecture: generality through pointer arithmetic, not rewriting logic.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Passing `from[i]` (value) instead of `from+i` (address) | Type error / wrong data passed | Pass shifted pointer `from + i` |
| Forgetting destination array must be large enough | Buffer overflow / UB | Ensure `to` has ≥ `j+n` elements |

### Quick Recall
- Shift the base pointer (`arr + i`) to reuse an index-0 function on any subarray.

---

## 8. In-Place Array Reversal 📅 Week 4

### Concept Summary
Reverse an array **without extra memory** using two pointers: one from the start, one from the end, swapping and moving inward until they cross. Relies on pointer increment/decrement and **relational comparison** (only valid within the same array).

### Key Syntax / Rules Box
```c
void reverse_array(int arr[], int n) {
    int *left = arr;
    int *right = arr + n - 1;
    while (left < right) {      // valid only: same-array comparison
        swap(left, right);       // swap(int*, int*) - dereference-based swap
        left++;
        right--;
    }
}
```
- Loop condition uses `<`/`>` — only well-defined when both pointers are in the **same array**.
- `==`/`!=` are valid for any same-type pointers, but `<`/`>` are undefined across different arrays.
- Odd-length array: middle element naturally skipped (never swapped with itself) once `left==right`.

### Detailed Code Example
```c
#include <stdio.h>
void swap(int *p1, int *p2) { int t=*p1; *p1=*p2; *p2=t; }
void reverse_array(int arr[], int n) {
    int *left = arr, *right = arr + n - 1;
    while (left < right) {   // stop when pointers meet/cross
        swap(left, right);
        left++;    // move toward middle from front
        right--;   // move toward middle from back
    }
}
int main() {
    int a[] = {101,21,-1,121,0,5};
    reverse_array(a, 6);
    for (int i=0;i<6;i++) printf("%d ", a[i]);
    return 0;
}
// Output: 5 0 121 -1 21 101
```

**What would NPTEL ask about this?**
- ❓ For an odd-length array (n=5), how many `swap` calls occur?
  ✅ 2 swaps (middle element untouched).
  💡 Loop runs while `left<right`; middle index makes `left==right`, loop stops before a self-swap.
- ❓ Is `ptrA < ptrB` well-defined if `ptrA` points into `array1` and `ptrB` into `array2`?
  ✅ No — undefined behavior.
  💡 Relational pointer comparison is only defined *within the same array*.
- ❓ What if `reverse_array` used `left <= right` instead of `left < right`?
  ✅ For even n, harmless (loop still stops correctly since they'd cross, never equal); for odd n, it would incorrectly re-swap the middle element with itself (self-swap has no bad effect, but the extra condition is redundant/risk-prone for other logic).
  💡 Tests understanding of the crossing condition, not just symptom-spotting.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Using extra array for reversal | Wastes O(n) memory | Use two-pointer in-place swap |
| Comparing pointers from different arrays | Undefined behavior | Only compare within the same array |
| Off-by-one in `right = arr+n` (forgetting `-1`) | Starts one past the array (UB on deref) | `right = arr + n - 1` |

### Quick Recall
- Two pointers converge inward, swapping; stop when `left < right` fails; same-array comparison only.

---

## 9. The `sizeof` Operator 📅 Week 4

### Concept Summary
`sizeof` returns the number of bytes a type/expression occupies — it's an **operator**, not a function, and its result is **machine-dependent**. It's the hidden engine behind pointer arithmetic: `ptr + i` is compiled as `ptr + i*sizeof(type)`.

### Key Syntax / Rules Box
```c
sizeof(int);           // e.g. 4 (machine-dependent)
sizeof(array_name);    // total bytes of whole array, NOT element count
sizeof(array)/sizeof(array[0]); // -> number of elements
```
- `sizeof` on an array gives TOTAL bytes, not element count — must divide by element size to get count.
- C does not guarantee fixed sizes for `int`/`float`/etc. — only relationships (e.g., `sizeof(long) >= sizeof(int)`).
- Formula: `byte_address(ptr+i) = byte_address(ptr) + i*sizeof(type_pointed_to)`.
- `array[i]` compiles to `*(array + i)`, and internally `i * sizeof(type)` bytes are skipped.
- Zero-indexing exists BECAUSE `array[0]` = `*(array+0)` = `*array` with zero offset — simplest possible case.

### Detailed Code Example
```c
#include <stdio.h>
int main() {
    int num[10];
    printf("%lu\n", sizeof(num));               // e.g. 40 (10 * 4 bytes)
    printf("%lu\n", sizeof(num)/sizeof(num[0])); // 10 (element count)
    printf("%lu %lu\n", sizeof(int), sizeof(char)); // e.g. 4 1
    return 0;
}
```

**What would NPTEL ask about this?**
- ❓ If `sizeof(int)==4` and `int a[20]`, what does `sizeof(a)` return?
  ✅ `80`
  💡 `sizeof(array)` = total bytes = count × element size, not the count itself.
- ❓ Why is `malloc(10*sizeof(int))` preferred over `malloc(40)`?
  ✅ Portability — `sizeof(int)` adapts to the machine, `40` assumes int is always 4 bytes.
  💡 Hardcoding sizes breaks on machines where `int` is a different width.
- ❓ Is `sizeof` a function call?
  ✅ No — it's a compile-time operator (despite parenthesis syntax).
  💡 Common misconception tested directly in MCQs.

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| Treating `sizeof(array)` as element count | Wrong count used, bugs in loops | Divide by `sizeof(element)` |
| Hardcoding type sizes (`*4` for int) | Non-portable, breaks on other machines | Always use `sizeof(type)` |
| Assuming `sizeof` is called at runtime like a function | Misunderstanding of C semantics | It's resolved at compile time for known types |

### Quick Recall
- `sizeof` = compile-time, machine-dependent byte count; drives all pointer-arithmetic scaling.

---

## 10. Returning Pointers from Functions: Stack vs Heap 📅 Week 4

### Concept Summary
Returning the address of a **local (stack) variable** creates a **dangling pointer** — that memory is destroyed the instant the function returns. The fix is **heap allocation** via `malloc`, which persists until explicitly `free`d by the programmer.

### Key Syntax / Rules Box
```c
#include <stdlib.h>
int* increment_bad(int n) {
    int temp = n + 1;     // on STACK
    return &temp;          // ❌ dangling pointer once function returns
}
int* increment_safe(int n) {
    int *ptr = (int*) malloc(sizeof(int)); // on HEAP
    if (ptr == NULL) return NULL;           // always check malloc success
    *ptr = n + 1;
    return ptr;                              // ✅ safe, persists after return
}
// caller:
// int *p = increment_safe(1);
// free(p);   // caller's responsibility to free
// p = NULL;  // avoid dangling pointer reuse
```
- Stack memory (local vars) is auto-destroyed on function return — never return `&local_var`.
- Heap memory (via `malloc`) persists until `free()` is called — ideal for data that must outlive the function.
- Always use `sizeof` inside `malloc` for portability: `malloc(n * sizeof(type))`.
- `malloc` returns `void*` — cast to the needed pointer type (e.g., `(int*)`).
- Always check `malloc`'s return for `NULL` (allocation failure).
- After `free(ptr)`, set `ptr = NULL` to avoid accidental reuse (dangling pointer).
- **Memory leak** = forgot to `free`; **double-free** = freed twice; **dangling pointer** = used after `free`.

### Detailed Code Example
```c
#include <stdio.h>
#include <stdlib.h>
int* increment_safe(int n) {
    int *ptr = (int*) malloc(sizeof(int)); // heap allocation, persists
    if (ptr == NULL) return NULL;           // check failure
    *ptr = n + 1;                            // store computed value on heap
    return ptr;                              // safe to return
}
int main() {
    int *p = increment_safe(1);
    if (p != NULL) {
        printf("%d\n", *p); // 2
        free(p);             // release heap memory
        p = NULL;             // avoid dangling pointer
    }
    return 0;
}
```

**What would NPTEL ask about this?**
- ❓ 
```c
int* f(int n){ int t=n; return &t; }
```
what's wrong?
  ✅ Returns address of a stack-local variable → dangling pointer, UB on use.
  💡 `t` is destroyed the moment `f` returns; the returned address is meaningless.
- ❓ Who is responsible for calling `free()` on heap memory allocated inside a function?
  ✅ The caller (whoever receives the returned pointer).
  💡 Ownership transfers via the returned pointer; heap memory isn't tied to any one function's lifetime.
- ❓ What happens if you `free(p)` twice?
  ✅ Undefined behavior (heap corruption, possible crash) — a "double free" error.
  💡 Set `p = NULL` after freeing to make a second accidental `free(NULL)` harmless (freeing NULL is safe/no-op).

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `return &local_var;` | Dangling pointer, UB | `malloc` on heap and return that pointer |
| Not checking `malloc` return | Crash on NULL dereference if allocation fails | `if (ptr == NULL) { handle error }` |
| Forgetting `free()` | Memory leak | Always `free` when done |
| Using pointer after `free()` | Dangling pointer UB | Set to `NULL` after freeing; don't reuse |

### Quick Recall
- Never return address of a local var; heap (`malloc`/`free`) is the only way to persist data beyond a function call.

---

## 11. Dynamic String Duplication (`malloc` in Practice) 📅 Week 4

### Concept Summary
A worked example combining strings + heap memory: to truly **copy** a string (not just copy the pointer), compute its length, `malloc(len+1)` bytes on the heap, copy characters, and manually append `'\0'`.

### Key Syntax / Rules Box
```c
char* duplicate(char *s) {
    int len = 0;
    for (int i = 0; s[i] != '\0'; i++) len++;      // find length (excl. \0)
    char *t = (char*) malloc((len + 1) * sizeof(char)); // +1 for '\0'!
    for (int i = 0; i < len; i++) t[i] = s[i];      // copy chars
    t[len] = '\0';                                    // manually terminate
    return t;                                          // heap ptr - safe to return
}
```
- Allocate `len + 1`, not just `len` — forgetting the `+1` leaves no room for `\0` (buffer overflow / bad string).
- Simply doing `char *copy = s;` does **NOT** duplicate — both point to the *same* memory (aliasing bug).
- Caller must eventually `free()` the returned pointer.

### Detailed Code Example
```c
#include <stdio.h>
#include <stdlib.h>
char* duplicate(char *s) {
    int len = 0;
    for (int i = 0; s[i] != '\0'; i++) len++;
    char *t = (char*) malloc((len + 1) * sizeof(char)); // room for len chars + '\0'
    for (int i = 0; i < len; i++) t[i] = s[i];
    t[len] = '\0';
    return t;
}
int main() {
    char original[] = "Hello";
    char *copy = duplicate(original);
    printf("%s\n", copy);  // Hello (independent copy)
    copy[0] = 'J';
    printf("%s %s\n", original, copy); // Hello Jello -- proves independence
    free(copy);
    return 0;
}
```

**What would NPTEL ask about this?**
- ❓ If `malloc(len * sizeof(char))` is used instead of `(len+1)`, what's the bug?
  ✅ No space for `'\0'` → writing `t[len]='\0'` overflows the allocated buffer (UB).
  💡 Off-by-one in heap allocation is a classic NPTEL trap.
- ❓ Does `char *copy = original;` (pointer assignment) create a true duplicate?
  ✅ No — both point to the same memory; modifying one modifies the "other."
  💡 Tests whether student understands pointer aliasing vs. actual duplication.
- ❓ After `duplicate()` returns, is `t` (the local pointer variable) still valid?
  ✅ The variable `t` itself is gone (stack), but the **heap memory it pointed to** persists and is now accessible via the returned pointer in `main`.
  💡 Distinguishes "the pointer variable's lifetime" from "the pointed-to memory's lifetime."

### Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|-------------|-----------------|
| `malloc(len * sizeof(char))` | No room for `\0`, buffer overflow | `malloc((len+1) * sizeof(char))` |
| `char *copy = s;` (aliasing) | Not a real copy — shared memory | Manually copy chars into new heap buffer |
| Forgetting `t[len] = '\0';` | Copy isn't a valid C string | Explicitly null-terminate after copying |

### Quick Recall
- Duplicate a string = `malloc(len+1)` + char-copy loop + manual `'\0'`; pointer assignment alone ≠ duplication.

---

## 🧪 Weekly Assignment Analysis

### Q1 — Generic Search Using Pointers
**Task:** Implement `int *find(int arr[], int n, int key);` — return a pointer to the **first occurrence** of `key`, or `NULL` if absent. The caller then uses pointer arithmetic (`ptr - arr` for index, `ptr < arr+n` to walk to the end) to report results.

**Solution:**
```c
int *find(int arr[], int n, int key) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == key)
            return &arr[i];   // address of first match
    }
    return NULL;              // not found
}
```

**Why this is correct:**
- The loop scans left-to-right, so the **first** `i` where `arr[i]==key` is guaranteed to be the first occurrence — returning immediately stops the search there.
- `&arr[i]` returns the **address** of that element (equivalent to `arr + i`), matching the required `int*` return type — this is NOT a dangling pointer because `arr` in `main` is a local array on `main`'s stack frame that is still alive when `find` returns (find's own stack frame dies, but it never pointed into its *own* locals — it points into the caller's array).
- Returning `NULL` when no match exists lets the caller distinguish "found at index 0" (a valid, non-NULL address) from "not found" — this is exactly why the function can't just return an index like `-1` as cleanly; `NULL` is the idiomatic "no pointer" sentinel.
- The caller's `ptr - arr` computes the index via **pointer subtraction** — subtracting two pointers into the same array yields the number of elements between them (this only works because `ptr` and `arr` point within the *same* array, same rule as Topic 8's relational comparisons).
- The trailing `while (ptr < arr + n) { ...; ptr++; }` walks from the found position to the end — `arr + n` is the safe one-past-the-end sentinel (valid for comparison, matching Topic 5's rule that `array+n` must never be *dereferenced*, only compared against).

**Why common wrong attempts fail:**
- Returning `i` (an `int`) instead of `&arr[i]` → type mismatch with the declared `int*` return type; won't compile cleanly or loses the pointer semantics the caller depends on.
- Not `break`-ing / returning immediately on match → would return the **last** occurrence instead of the first if the loop kept scanning and overwrote the pointer.
- Returning `0` instead of `NULL` on failure → works in practice since `NULL` is often `0`, but `NULL` is the correct, portable, self-documenting idiom for "no valid pointer."

---

### Q2 — Remove Duplicate Elements (Preserve First-Occurrence Order)
**Task:** Read `n` integers, print only each value's **first occurrence**, preserving original order, without disturbing the underlying array.

**Solution:**
```c
for (int i = 0; i < n; i++) {
    int duplicate = 0;
    for (int j = 0; j < i; j++) {          // only look BACKWARD, at earlier elements
        if (arr[i] == arr[j]) {
            duplicate = 1;
            break;
        }
    }
    if (!duplicate) printf("%d ", arr[i]);
}
```

**Why this is correct:**
- For each element `arr[i]`, the inner loop checks only indices `j < i` (everything *before* it). If `arr[i]` matches any earlier element, it has already been printed once, so it's skipped (`duplicate = 1`).
- Because the inner loop only looks backward, the very **first** time a value appears, no earlier match exists, `duplicate` stays `0`, and it prints — this is precisely what guarantees "preserve order of first occurrence."
- `break` on the first match is an optimization (no need to keep scanning once duplication is confirmed) — it doesn't change correctness either way.
- This is an O(n²) approach, which is fine given the constraint `n ≤ 100`.

**Why common wrong attempts fail:**
- Checking `j < n` (the whole array) instead of `j < i` → every value would find *itself* or a later duplicate match and could wrongly suppress **all** copies, including the first — the search window must be restricted to *earlier* elements only.
- Sorting the array first to "group" duplicates → breaks the required "preserve original order" constraint, since sorting rearranges elements.
- Using a frequency array indexed directly by value (like Q3's technique) → doesn't work here in general because array elements can be *any* int (including negatives or large values), unlike Q3's constrained A–Z range; a frequency array would need value-to-index mapping or a hash-based structure instead.

---

### Q3 — Check if Two Strings Are Anagrams
**Task:** Given two same-length strings of uppercase letters (A–Z), determine if they're anagrams (same letters, same frequencies, any order).

**Solution:**
```c
int freq1[26] = {0}, freq2[26] = {0};
for (i = 0; i < n; i++) {
    freq1[str1[i] - 'A']++;   // map 'A'..'Z' -> index 0..25
    freq2[str2[i] - 'A']++;
}
for (i = 0; i < 26; i++) {
    if (freq1[i] != freq2[i]) { printf("0"); return 0; }
}
printf("1");
```

**Why this is correct:**
- `str1[i] - 'A'` exploits the fact that uppercase letters are **contiguous** ASCII values (`'A'`=65 … `'Z'`=90). Subtracting `'A'` maps any letter to a **0–25 index**, which is a classic "char arithmetic" trick tying directly into Topic 2/3's character-array/ASCII concepts.
- Both `freq1[]` and `freq2[]` are initialized with `= {0}` (partial initializer, Topic 2's rule) — this guarantees all 26 counts start at zero, not junk values, before counting begins.
- Two strings are anagrams **iff** every letter occurs the same number of times in both — comparing the two frequency arrays element-by-element directly implements this definition.
- Because `n` is given and both strings are guaranteed the same length (per constraints), there's no need to separately check lengths — the frequency comparison alone is sufficient.
- `%s` with `scanf` (no `&` needed, since `str1`/`str2` are arrays that decay to pointers — Topic 4's array-name-as-pointer rule) reads a whitespace-terminated token into the char array, which `scanf` automatically null-terminates.

**Why common wrong attempts fail:**
- Sorting both strings and comparing them directly → also a valid alternative approach, but if implemented naively (e.g., via nested loops) is O(n²) or requires a sorting function not covered yet; the frequency-count method is O(n) and matches the char-array/array-indexing techniques from this week.
- Forgetting to initialize `freq1`/`freq2` to `{0}` → arrays would start with junk values (Topic 2's "uninitialized array = garbage" pitfall), corrupting every comparison.
- Comparing `str1[i] == str2[i]` position-by-position → checks if the strings are **identical**, not anagrams; anagrams can have letters in a completely different order, so position-wise comparison is the wrong check entirely.
- Off-by-one on the char-to-index mapping (e.g., forgetting `- 'A'`) → would try to index `freq1[]`/`freq2[]` with values like 65–90 instead of 0–25, causing an out-of-bounds array access (undefined behavior, ties back to Topic 2's "arrays have no automatic bounds checking" rule).
