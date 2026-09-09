# 📘 NPTEL: Programming in Modern C++ — Week 1 Notes
**Prof. Partha Pratim Das | IIT Kharagpur**
**Modules: M01 · M02 · M03 · M04 · M05 · Tutorial T01**

> ⚠️ These notes skip all administrative/history content and focus only on exam-testable concepts.

---

## Table of Contents
1. [C vs C++ I/O — `iostream`, `cin`, `cout`](#topic-1)
2. [Namespace `std` & Header Conventions](#topic-2)
3. [Variable Declaration Differences (C vs C++)](#topic-3)
4. [`bool` in C and C++](#topic-4)
5. [Arrays vs `std::vector`](#topic-5)
6. [C-Strings (`string.h`) vs C++ `std::string`](#topic-6)
7. [Sorting — Bubble Sort, `std::sort`, `qsort`](#topic-7)
8. [Searching — `bsearch` vs `std::binary_search`](#topic-8)
9. [`<algorithm>` Library — `replace`, `rotate`](#topic-9)
10. [Stack in C (Manual) vs C++ `std::stack`](#topic-10)
11. [STL Containers Overview](#topic-11)
12. [C Preprocessor (CPP) — Macros, `#define`, `#undef`](#topic-12)
13. [Conditional Compilation — `#ifdef`, `#if`, `#ifndef`](#topic-13)
14. [`#include` Guards & Circular Inclusion](#topic-14)
15. [Predefined Macros — `__LINE__`, `__FILE__`, `__cplusplus`](#topic-15)

---

<a name="topic-1"></a>
### 1. C vs C++ I/O — `iostream`, `cin`, `cout` `📅 Week 1`

#### 1. 📌 What & Why
- C uses `printf`/`scanf` from `<stdio.h>`; C++ introduces **stream-based I/O** via `<iostream>`
- `std::cout` is an **output stream object**; `<<` is the **stream insertion operator**
- `std::cin` is an **input stream object**; `>>` is the **stream extraction operator**
- No need for format specifiers (`%d`, `%f`) — types are inferred automatically
- Standard from the beginning of C++ (`<iostream>` is not tagged as a new feature — it is base C++)

#### 2. 🔤 Syntax Reference
```cpp
#include <iostream>       // C++ I/O header (no .h)
using namespace std;      // so we don't write std:: everywhere

// Output
cout << "text" << variable << endl;   // endl flushes buffer + newline
cout << "text" << "\n";               // \n does NOT flush buffer

// Input
cin >> variable;          // reads one value
cin >> a >> b;            // chained: reads two values

// Formatting (default precision)
// C printf: 6 decimal places for double
// C++ cout: 5 significant digits for double (DIFFERENT!)
```
- `endl` = newline + buffer flush (a **stream manipulator functor**)
- `\n` = just newline character (faster, no flush)
- `std::cout` is an `ostream`; `std::cin` is an `istream`

#### 3. 💻 Code Example (Detailed)
```cpp
// Program 02.01 / 02.02 / 02.03 — from lecture
#include <iostream>
#include <cmath>          // C math library in C++ style (cmath, not math.h)
using namespace std;

int main() {
    // Hello World
    cout << "Hello World in C++" << endl;  // endl = \n + flush

    // Add Two Numbers — no & needed (unlike scanf)
    int a, b;
    cout << "Input two numbers:\n";
    cin >> a >> b;             // chained input, type-safe
    int sum = a + b;           // can declare ANYWHERE (unlike C89)
    cout << "Sum of " << a << " and " << b << " is: " << sum << endl;

    // Square Root — note precision difference!
    double x;
    cin >> x;
    double sqrt_x = sqrt(x);  // from <cmath>
    cout << "Sq. Root of " << x << " is: " << sqrt_x << endl;
    // C printf: 2.000000 is: 1.414214  (6 decimal places)
    // C++ cout: 2 is: 1.41421          (5 significant digits)
    return 0;
}
```

**🎯 NPTEL will ask:**
| # | Question | Answer | Why |
|---|----------|--------|-----|
| 1 | What is the output of `cout << 2.0`? | `2` | Default cout precision is 5 sig figs; trailing zeros dropped |
| 2 | What is the output of `printf("%lf", 2.0)`? | `2.000000` | printf default precision is 6 decimal places |
| 3 | What does `endl` do that `\n` does NOT? | Flushes the output buffer | `endl` is a manipulator that calls `flush` |
| 4 | What does `cin >> a >> b` require as input for a=3, b=4? | `3 4` or `3\n4` | `>>` skips whitespace/newlines |
| 5 | Which header contains `sqrt` in C++? | `<cmath>` | C math in C++ = prefix `c`, no `.h` |

#### 4. 📊 Comparison Table
| Aspect | C | C++ |
|--------|---|-----|
| I/O Header | `<stdio.h>` | `<iostream>` |
| Output | `printf("text %d", x)` | `cout << "text " << x` |
| Input | `scanf("%d", &x)` (needs `&`) | `cin >> x` (no `&`) |
| Format specifier | Required (`%d`, `%lf`) | Not needed (type deduced) |
| Type safety | ❌ Unsafe (void*) | ✅ Type-safe |
| Default double precision | 6 decimal places | 5 significant digits |
| Newline | `\n` or `printf("\n")` | `endl` (flush) or `"\n"` |

#### 5. ⚠️ Pitfalls
| Common Mistake | What Goes Wrong | Correct Approach |
|---------------|----------------|-----------------|
| Using `<iostream.h>` | Deprecated — may compile but disastrous | Use `<iostream>` (no `.h`) |
| Expecting `cout << 2.0` to print `2.000000` | Prints `2` (5 sig figs, not 6 decimal) | Use `setprecision()` if needed |
| Forgetting `&` in scanf | Undefined behavior / segfault | `scanf("%d", &x)` — C always needs `&` |
| Using `\n` instead of `endl` for interactive programs | Buffer not flushed, output may not appear | Use `endl` for prompts |

#### 6. ⚡ Quick Recall
- `cout <<` = output, `cin >>` = input
- `endl` = newline + flush; `\n` = just newline
- C++ cout default precision: **5 significant digits** (not 6 like printf)
- No format specifiers, no `&` in `cin >>` (unlike scanf)
- `<iostream>` not `<iostream.h>` (latter is deprecated)

---

<a name="topic-2"></a>
### 2. Namespace `std` & Header Conventions `📅 Week 1`

#### 1. 📌 What & Why
- All C++ Standard Library names live inside the `std` **namespace** to avoid name collisions
- C Standard Library headers are available in C++ with a `c` prefix and no `.h`
- `using namespace std;` brings all std names into scope so you don't write `std::` repeatedly
- Problem `using namespace std;` solves: avoids writing `std::cout`, `std::endl`, `std::cin` everywhere

#### 2. 🔤 Syntax Reference
```cpp
// Without using
std::cout << "Hello" << std::endl;

// With using namespace std
using namespace std;
cout << "Hello" << endl;  // std:: not needed

// C header in C++ — prefix 'c', no .h, names in std::
#include <cmath>    // instead of <math.h>
#include <cstring>  // instead of <string.h>
#include <cstdio>   // instead of <stdio.h>
std::sqrt(5.0);     // in std namespace

// NOT preferred (but compiles):
#include <math.h>   // names NOT in std namespace
sqrt(5.0);          // global — no std::
```

#### 3. 💻 Code Example (Detailed)
```cpp
#include <iostream>    // C++ standard header: no .h
#include <cmath>       // C math library in C++ style
using namespace std;   // Bring std namespace into scope

int main() {
    double x = 2.0;
    cout << sqrt(x) << endl;  // sqrt from cmath, via 'using'
    return 0;
}
```

**🎯 NPTEL will ask:**
| # | Question | Answer | Why |
|---|----------|--------|-----|
| 1 | What is the C++ equivalent of `<string.h>`? | `<cstring>` | Prefix `c`, remove `.h`, names go into `std::` |
| 2 | What happens if you write `#include <iostream.h>`? | Compilation may fail or behave unexpectedly | `.h` for C++ headers is deprecated |
| 3 | Is `sqrt` in `std::` when you use `#include <math.h>`? | No | Only `<cmath>` puts it in `std::` |

#### 4. 📊 Comparison Table
| Header Type | C | C++ (Preferred) |
|-------------|---|-----------------|
| C Std library | `<stdio.h>` | `<cstdio>` (in `std::`) |
| C++ std library | N/A | `<iostream>` (no `.h`) |
| Math | `<math.h>` | `<cmath>` |
| String (C-style) | `<string.h>` | `<cstring>` |
| C++ string type | N/A | `<string>` |

#### 5. ⚠️ Pitfalls
| Common Mistake | What Goes Wrong | Correct Approach |
|---------------|----------------|-----------------|
| `#include <iostream.h>` | Deprecated — disaster | `#include <iostream>` |
| `#include <math.h>` then `std::sqrt()` | Compile error — not in `std::` with `.h` | Use `<cmath>` |
| Forgetting `using namespace std;` | Must write `std::` everywhere | Add `using namespace std;` after includes |

#### 6. ⚡ Quick Recall
- C++ std names are in `std` namespace (unlike C, which is global)
- `using namespace std;` removes the need to write `std::` prefix
- C header in C++: add `c`, remove `.h` → `math.h` → `cmath`
- `<iostream.h>` is deprecated — never use it
- `std::cout`, `std::cin`, `std::endl` are the qualified names

---

<a name="topic-3"></a>
### 3. Variable Declaration Differences (C vs C++) `📅 Week 1`

#### 1. 📌 What & Why
- In **C89/K&R C**: all variables must be declared at the **beginning of a block** (before any statements)
- **C99** allowed declarations anywhere; **C++** has always allowed declarations anywhere
- C++ additionally allows declaring loop variables **inside the `for` statement** — the variable's scope is the loop
- This is a key exam trap: C89 code with mid-block declarations is **invalid in C89** but valid in C++

#### 2. 🔤 Syntax Reference
```cpp
// C89 style (ONLY valid way in K&R / C89)
int i, n;      // ALL declarations at top
int sum = 0;
// ... statements ...

// C99 / C++ style — declare anywhere
int sum = 0;
cin >> n;
int result = sum + n;  // declaration after a statement — OK in C++

// C++ for-loop: declare loop variable IN the for
for (int i = 0; i < n; ++i) {  // i is LOCAL to the loop
    sum += i;
}
// i is OUT OF SCOPE here — cannot use i after loop
```
- The `for`-loop variable declared inside `for(int i...)` has **loop-local scope**
- This is valid in C99 too, but NOT in C89

#### 3. 💻 Code Example (Detailed)
```cpp
// Program 02.04: Sum of n numbers
#include <iostream>
using namespace std;

int main() {
    int n;         // declared at top (like C)
    int sum = 0;   // OK to initialize here

    cout << "Input limit:" << endl;
    cin >> n;

    // i declared INSIDE the for — C++ (and C99) style
    for (int i = 0; i <= n; ++i)
        sum = sum + i;
    // i is not accessible here

    cout << "Sum of " << n << " numbers is: " << sum << endl;
    return 0;
}
```

**🎯 NPTEL will ask:**
| # | Question | Answer | Why |
|---|----------|--------|-----|
| 1 | Can you declare `int i` inside `for(int i=0; ...)` in C89? | No | C89 requires all declarations at block top |
| 2 | What is the scope of `i` in `for(int i=0; i<5; i++)`? | Only inside the for loop | Loop variable scope ends with loop |
| 3 | Is `int sum = a + b;` valid in C89 if `a, b` are declared above? | No — if there are statements before it | In C89, no declarations after any statement |

#### 4. 📊 Comparison Table
| Feature | C89/K&R | C99 | C++ |
|---------|---------|-----|-----|
| Declare anywhere | ❌ | ✅ | ✅ |
| `for(int i=0;...)` | ❌ | ✅ | ✅ |
| Init in declaration | Partial | ✅ | ✅ |

#### 5. ⚠️ Pitfalls
| Common Mistake | What Goes Wrong | Correct Approach |
|---------------|----------------|-----------------|
| Using `i` after a for loop in which `i` was declared inside the for | Compile error | Declare `i` outside the loop if you need it after |
| Thinking C99 and C89 are the same | C89 requires top-of-block declarations | Know which standard is being tested |

#### 6. ⚡ Quick Recall
- C89: declare ALL variables at the **start** of a block
- C++ (and C99): declare **anywhere**, including inside `for`
- `for(int i=0; ...)` — `i` is local to the loop
- C++ always allowed mid-block declarations; C99 added this to C

---

<a name="topic-4"></a>
### 4. `bool` in C and C++ `📅 Week 1`

#### 1. 📌 What & Why
- `bool` is a **built-in type** in C++: `true` (literal) and `false` (literal)
- In C before C99: no `bool` type — programmers used `int` with `#define TRUE 1 / FALSE 0`
- C99 added `<stdbool.h>` which defines `bool` (expands to `_Bool`), `true` (expands to 1), `false` (expands to 0)
- In C++: no extra header needed, `bool`, `true`, `false` are keywords/literals

#### 2. 🔤 Syntax Reference
```cpp
// C++ — no header needed
bool x = true;       // true is a literal keyword
bool y = false;      // false is a literal keyword
cout << x;           // outputs: 1  (bool prints as int by default)
cout << boolalpha << x; // outputs: true (with manipulator)

// C with stdbool.h
#include <stdbool.h>
bool x = true;       // bool → _Bool, true → 1
printf("%d", x);     // outputs: 1
```
- `cout << bool_var` prints **1 or 0** by default (not "true"/"false")
- Use `boolalpha` manipulator for "true"/"false" text output

#### 3. 💻 Code Example (Detailed)
```cpp
// Program 02.05 comparison across C/C++
#include <iostream>
using namespace std;

int main() {
    bool x = true;         // bool is built-in in C++
    cout << "bool is " << x;  // Prints: bool is 1
    return 0;
}
// Output: bool is 1
```

**🎯 NPTEL will ask:**
| # | Question | Answer | Why |
|---|----------|--------|-----|
| 1 | What does `cout << true` print? | `1` | bool outputs as int by default |
| 2 | What header is needed for `bool` in C (C99)? | `<stdbool.h>` | C99 added bool via stdbool.h |
| 3 | Is `bool` a keyword in C++? | Yes | Built-in type — no header needed |
| 4 | What does `#define TRUE 1` expand to? | `1` (integer) | Old C way: no true bool type |

#### 4. 📊 Comparison Table
| Feature | C (pre-C99) | C (C99) | C++ |
|---------|-------------|---------|-----|
| `bool` type | ❌ (use `int`) | ✅ via `<stdbool.h>` | ✅ built-in keyword |
| `true`/`false` | `#define TRUE 1` | macros expanding to 1/0 | built-in literals |
| Header needed | None (use int) | `<stdbool.h>` | None |

#### 5. ⚠️ Pitfalls
| Common Mistake | What Goes Wrong | Correct Approach |
|---------------|----------------|-----------------|
| Expecting `cout << true` to print `"true"` | Prints `1` | Add `<< boolalpha` before printing |
| Using `#define TRUE 1` in C++ | Works but unnecessary | Use `true` keyword directly |

#### 6. ⚡ Quick Recall
- C++: `bool`, `true`, `false` are built-in — no header
- C99: need `#include <stdbool.h>`
- C pre-C99: use `int` and `#define TRUE 1 / FALSE 0`
- `cout << true` prints `1`, not `"true"`

---

<a name="topic-5"></a>
### 5. Arrays vs `std::vector` `📅 Week 1`

#### 1. 📌 What & Why
- C arrays: fixed size, must be known at compile time (or use `malloc` for dynamic)
- C++ `std::vector`: **dynamically resizable**, type-safe, part of STL, from `<vector>`
- `vector<int> arr(MAX)` creates a vector of `MAX` ints (size at definition time)
- `arr.resize(count)` can resize **at run time** — cleaner than `malloc/realloc`
- `arr.size()` returns current size — no need to track size manually

#### 2. 🔤 Syntax Reference
```cpp
#include <vector>
using namespace std;

// Fixed size at definition
vector<int> v(100);         // 100 ints, initialized to 0

// Default (empty), then resize
vector<int> v;              // empty vector
v.resize(count);            // set size at run-time

// Access (same as array)
v[0] = 10;                  // 0-indexed access
v.size();                   // returns current size (unsigned)

// Comparison
int arr[100];               // C array: fixed, no size method
vector<int> v(100);         // C++ vector: dynamic, has size()
```

#### 3. 💻 Code Example (Detailed)
```cpp
// Program 03.03 / 03.04 — vector usage
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int count, sum = 0;
    cout << "Enter the no. of elements: ";
    cin >> count;

    // METHOD 1: Fixed-size vector (like #define MAX 100 in C)
    // vector<int> arr(MAX);

    // METHOD 2: Default empty + resize at run-time
    vector<int> arr;         // empty, size=0
    arr.resize(count);       // NOW it has 'count' slots

    for (int i = 0; i < arr.size(); i++) {
        arr[i] = i;
        sum += arr[i];
    }
    cout << "Array Sum: " << sum << endl;
    return 0;
}
// Enter the no. of elements: 10
// Array Sum: 45
```

**🎯 NPTEL will ask:**
| # | Question | Answer | Why |
|---|----------|--------|-----|
| 1 | What header is needed for `vector`? | `<vector>` | STL container header |
| 2 | What does `vector<int> arr;` create? | Empty vector of ints (size 0) | Default constructor creates empty vector |
| 3 | How does `arr.resize(n)` differ from `malloc(n*sizeof(int))`? | resize is type-safe and automatic | malloc returns `void*`, needs cast and sizeof |
| 4 | What does `arr.size()` return? | Number of elements (unsigned `size_t`) | Member function — unlike C where you track manually |

#### 4. 📊 Comparison Table
| Aspect | C Array | C++ vector |
|--------|---------|-----------|
| Size fixed | At compile time (or #define) | Can resize at run-time |
| Dynamic alloc | `malloc` + `free` (manual) | `resize()` (automatic) |
| Size tracking | Manual variable | `v.size()` |
| Type safety | ❌ (malloc is void*) | ✅ |
| Header | None | `<vector>` |

#### 5. ⚠️ Pitfalls
| Common Mistake | What Goes Wrong | Correct Approach |
|---------------|----------------|-----------------|
| `vector<int> v;` then accessing `v[0]` without resize | Undefined behavior — size is 0 | Call `v.resize(n)` or `v.push_back(x)` first |
| Comparing `v.size()` with `int` in condition | Signed/unsigned comparison warning | Cast or use `(int)v.size()` |

#### 6. ⚡ Quick Recall
- `vector<T> v(n)` — vector of n elements (size set at definition)
- `vector<T> v; v.resize(n)` — resize at run-time
- `v.size()` — returns current number of elements
- No need for `malloc`/`free` — managed automatically
- `#include <vector>` required

---

<a name="topic-6"></a>
### 6. C-Strings (`string.h`) vs C++ `std::string` `📅 Week 1`

#### 1. 📌 What & Why
- C-strings: `char[]` arrays terminated by `\0` (NULL character); manipulated by `string.h` functions
- C++ `std::string`: a **class type** in `<string>`; supports operators (`+`, `=`, `<`, `>`)
- Key advantage: `str1 + str2` in C++ vs `strcpy(str, str1); strcat(str, str2);` in C
- C++ also provides all `<cstring>` functions (`strcpy`, `strlen`, etc.) in the `std` namespace

#### 2. 🔤 Syntax Reference
```cpp
// C++ string
#include <string>
using namespace std;

string s1 = "HELLO ";
string s2 = "WORLD";
string s3 = s1 + s2;    // concatenation with operator+
s1 = s2;                // assignment with operator= (like strcpy)
bool eq = (s1 == s2);   // comparison with == (like strcmp)
bool lt = (s1 < s2);    // lexicographic < (like strcmp < 0)
int len = s1.size();    // or s1.length() — like strlen()
s1.c_str();             // returns const char* for C interop

// C string
char str1[] = {'H','E','L','L','O',' ','\0'}; // manual null terminator
char str2[] = "WORLD";   // auto null-terminated
char str[20];
strcpy(str, str1);        // copy str1 into str
strcat(str, str2);        // append str2 to str
```

#### 3. 💻 Code Example (Detailed)
```cpp
// Program 03.05 — String Concatenation
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str1 = "HELLO ";  // C++ string — auto-managed memory
    string str2 = "WORLD";

    string str = str1 + str2; // + operator does concatenation
                               // NO need for strcpy/strcat
                               // NO need to pre-size a buffer

    cout << str;   // HELLO WORLD
    return 0;
}
```

**🎯 NPTEL will ask:**
| # | Question | Answer | Why |
|---|----------|--------|-----|
| 1 | What is the C++ equivalent of `strcat`? | `operator+` or `operator+=` | C++ string class overloads these operators |
| 2 | What is the C++ equivalent of `strcmp`? | Relational operators `==`, `<`, `>`, `<=`, `>=` | String class overloads comparison operators |
| 3 | What is the C++ equivalent of `strcpy`? | `operator=` | Assignment operator copies the string |
| 4 | What does `c_str()` return? | `const char*` — null-terminated C string | Needed for C interop functions |
| 5 | What header is needed for C++ `string`? | `<string>` (not `<string.h>`) | `<string.h>` is the C header |

#### 4. 📊 Comparison Table
| Operation | C (`string.h`) | C++ (`<string>`) |
|-----------|----------------|-----------------|
| Copy | `strcpy(dst, src)` | `dst = src` |
| Concatenate | `strcat(dst, src)` | `dst + src` or `dst += src` |
| Compare | `strcmp(a, b)` → -1/0/+1 | `a == b`, `a < b`, etc. → bool |
| Length | `strlen(s)` | `s.size()` or `s.length()` |
| Substring | `strncpy` | `s.substr(pos, len)` |
| Find | `strstr`, `strchr` | `s.find(...)` |
| Header | `<string.h>` or `<cstring>` | `<string>` |

#### 5. ⚠️ Pitfalls
| Common Mistake | What Goes Wrong | Correct Approach |
|---------------|----------------|-----------------|
| Forgetting `'\0'` in C char array initializer | String not properly terminated | `char s[] = {'A','B','\0'};` or `char s[] = "AB";` |
| Using `<string.h>` for C++ `string` type | Wrong header — `string.h` gives C functions | Use `<string>` for C++ `std::string` |
| Buffer too small in `strcat` | Buffer overflow / undefined behavior | C++ `string` handles memory automatically |

#### 6. ⚡ Quick Recall
- C string = `char[]` + `'\0'` + `<string.h>` functions
- C++ `string` = class in `<string>`, supports `+`, `=`, `==`, `<`, etc.
- `+` for concatenation replaces `strcat`
- `=` replaces `strcpy`
- `==`, `<`, `>` replace `strcmp` comparisons
- `s.c_str()` converts `std::string` to `const char*` for C interop

---

<a name="topic-7"></a>
### 7. Sorting — Bubble Sort, `std::sort`, `qsort` `📅 Week 1`

#### 1. 📌 What & Why
- C standard library provides `qsort` from `<stdlib.h>` — type-unsafe (uses `void*`)
- C++ `<algorithm>` provides `std::sort` — type-safe, no `sizeof` needed, cleaner comparator
- `std::sort` with no comparator: **ascending order** by default
- With a comparator function: any custom order (e.g., descending)

#### 2. 🔤 Syntax Reference
```cpp
#include <algorithm>
using namespace std;

// Default sort (ascending)
sort(data, data + n);             // start pointer, past-end pointer

// Custom sort (descending) — comparator returns bool
bool compare(int i, int j) { return (i > j); }  // type-safe
sort(data, data + n, compare);

// C qsort (for comparison)
#include <stdlib.h>
int compare(const void* a, const void* b) {  // type-UNSAFE
    return (*(int*)a < *(int*)b);            // cast needed
}
qsort(data, n, sizeof(int), compare);        // sizeof needed
```
- `std::sort` comparator: `bool cmp(T a, T b)` — return `true` if `a` should come before `b`
- `qsort` comparator: `int cmp(const void*, const void*)` — return negative/0/positive

#### 3. 💻 Code Example (Detailed)
```cpp
// Program 04.02 / 04.03 — Sorting comparison
#include <iostream>
#include <algorithm>
using namespace std;

// Descending comparator — type-safe, no cast needed
bool compare(int i, int j) {
    return (i > j);   // true if i should come before j
}

int main() {
    int data[] = {32, 71, 12, 45, 26};

    // Ascending (default)
    sort(data, data + 5);          // no comparator needed
    for (int i = 0; i < 5; i++)
        cout << data[i] << " ";
    // Output: 12 26 32 45 71

    // Reset and sort descending
    int data2[] = {32, 71, 12, 45, 26};
    sort(data2, data2 + 5, compare);
    for (int i = 0; i < 5; i++)
        cout << data2[i] << " ";
    // Output: 71 45 32 26 12

    return 0;
}
```

**🎯 NPTEL will ask:**
| # | Question | Answer | Why |
|---|----------|--------|-----|
| 1 | What is the default sort order of `std::sort`? | Ascending | Default comparator uses `operator<` |
| 2 | What header contains `std::sort`? | `<algorithm>` | STL algorithm library |
| 3 | Why is `qsort` considered type-unsafe? | It uses `void*` and requires manual casting | `(*(int*)a < *(int*)b)` — must cast from void* |
| 4 | What does `sort(data, data+5)` mean? | Sort from `data[0]` to `data[4]` | `data+5` is past-the-end (exclusive) |
| 5 | What does `sort(data, data+5, compare)` return? | Nothing (void) — sorts in-place | Modifies the array directly |

#### 4. 📊 Comparison Table
| Aspect | `qsort` (C) | `std::sort` (C++) |
|--------|-------------|------------------|
| Header | `<stdlib.h>` | `<algorithm>` |
| Comparator signature | `int cmp(const void*, const void*)` | `bool cmp(T, T)` |
| Type safety | ❌ void* casts needed | ✅ type-safe |
| Size argument | Needs `sizeof(element)` | Inferred from type |
| Range | start, count, sizeof, cmp | start, end, cmp |

#### 5. ⚠️ Pitfalls
| Common Mistake | What Goes Wrong | Correct Approach |
|---------------|----------------|-----------------|
| `sort(data, data+5)` but data is unsorted after | sort is in-place, check the array after | The array IS sorted — check print loop |
| Comparator returns `>=` instead of `>` for descending | Undefined behavior (strict weak ordering violated) | Return strictly `i > j` |

#### 6. ⚡ Quick Recall
- `std::sort(begin, end)` — ascending, from `<algorithm>`
- `std::sort(begin, end, cmp)` — custom comparator
- `cmp(a, b)` returns `true` if `a` should come before `b`
- `sort` takes pointers: `sort(arr, arr+n)` where `n` = element count
- `qsort` is type-unsafe; `sort` is type-safe (no `sizeof`, no `void*`)

---

<a name="topic-8"></a>
### 8. Searching — `bsearch` vs `std::binary_search` `📅 Week 1`

#### 1. 📌 What & Why
- C: `bsearch` from `<stdlib.h>` — type-unsafe, requires comparator with `void*`
- C++: `std::binary_search` from `<algorithm>` — type-safe, no comparator needed for basic use
- **Array must be sorted** before binary search (both in C and C++)
- `binary_search` returns `bool` (found/not found); `bsearch` returns a pointer to the element or NULL

#### 2. 🔤 Syntax Reference
```cpp
#include <algorithm>

// Requires sorted array
int data[] = {1, 2, 3, 4, 5};
int k = 3;

bool found = binary_search(data, data+5, k);  // type-safe, no cast
// returns true if found, false otherwise

// C bsearch
#include <stdlib.h>
int compare(const void* a, const void* b) {
    if (*(int*)a < *(int*)b) return -1;
    if (*(int*)a == *(int*)b) return 0;
    return 1;
}
void* result = bsearch(&k, data, 5, sizeof(int), compare);
// returns pointer to element if found, NULL if not found
```

#### 3. 💻 Code Example (Detailed)
```cpp
// Program 04.04 — Binary Search
#include <iostream>
#include <algorithm>
using namespace std;

int main() {
    int data[] = {1, 2, 3, 4, 5};  // MUST be sorted
    int k = 3;

    if (binary_search(data, data + 5, k))
        cout << "found!" << endl;
    else
        cout << "not found" << endl;
    // Output: found!
    return 0;
}
```

**🎯 NPTEL will ask:**
| # | Question | Answer | Why |
|---|----------|--------|-----|
| 1 | What does `binary_search` return? | `bool` (true/false) | Unlike `bsearch` which returns a pointer |
| 2 | What does `bsearch` return when element is not found? | `NULL` (nullptr) | It returns `void*` to found element or NULL |
| 3 | Is a sorted array required for binary search? | Yes | Binary search only works on sorted data |
| 4 | What header contains `binary_search`? | `<algorithm>` | STL algorithm library |

#### 4. 📊 Comparison Table
| Aspect | `bsearch` (C) | `binary_search` (C++) |
|--------|--------------|----------------------|
| Return type | `void*` (pointer or NULL) | `bool` |
| Type safety | ❌ (void* casts) | ✅ |
| Comparator | Required (complex) | Optional (uses `<` by default) |
| Header | `<stdlib.h>` | `<algorithm>` |

#### 5. ⚡ Quick Recall
- `binary_search(begin, end, value)` → `bool`
- Array **must be sorted** before calling
- From `<algorithm>`; no comparator needed for basic use
- C `bsearch` → returns `void*`; C++ `binary_search` → returns `bool`

---

<a name="topic-9"></a>
### 9. `<algorithm>` Library — `replace`, `rotate` `📅 Week 1`

#### 1. 📌 What & Why
- `<algorithm>` provides many ready-to-use operations on ranges (arrays, vectors)
- `replace(begin, end, old_val, new_val)` — replaces all occurrences of `old_val` with `new_val`
- `rotate(begin, new_begin, end)` — left-rotates the range so `new_begin` becomes the first element
- Other useful functions: `merge`, `swap`, `remove`, `find`, `count`, `min`, `max`

#### 2. 🔤 Syntax Reference
```cpp
#include <algorithm>
using namespace std;

int data[] = {1, 2, 3, 4, 5};

// Replace all 3s with 2s
replace(data, data+5, 3, 2);
// data = {1, 2, 2, 4, 5}

// Rotate: make data[2] (value 3) the new first element
int data2[] = {1, 2, 3, 4, 5};
rotate(data2, data2+2, data2+5);
// data2 = {3, 4, 5, 1, 2}
// The element at data2+2 becomes [0]
```

#### 3. 💻 Code Example (Detailed)
```cpp
// Program 04.05 — replace and rotate
#include <iostream>
#include <algorithm>
using namespace std;

int main() {
    int data[] = {1, 2, 3, 4, 5};

    replace(data, data+5, 3, 2);  // replace value 3 with value 2
    for(int i = 0; i < 5; ++i)
        cout << data[i] << " ";
    // Output: 1 2 2 4 5

    int data2[] = {1, 2, 3, 4, 5};
    rotate(data2, data2+2, data2+5);  // rotate left, 3rd element becomes 1st
    for(int i = 0; i < 5; ++i)
        cout << data2[i] << " ";
    // Output: 3 4 5 1 2

    return 0;
}
```

**🎯 NPTEL will ask:**
| # | Question | Answer | Why |
|---|----------|--------|-----|
| 1 | What is the output of `rotate(data, data+2, data+5)` on `{1,2,3,4,5}`? | `3 4 5 1 2` | `data+2` (value 3) becomes the first element |
| 2 | What does `replace(data, data+5, 3, 2)` do to `{1,2,3,4,5}`? | `{1,2,2,4,5}` | Replaces ALL occurrences of 3 with 2 |

#### 6. ⚡ Quick Recall
- `replace(begin, end, old, new)` — replaces all matching values
- `rotate(begin, new_first, end)` — `new_first` element becomes index 0
- Both from `<algorithm>`
- Think of `rotate` as: "circular shift left until `new_first` is at front"

---

<a name="topic-10"></a>
### 10. Stack in C (Manual) vs C++ `std::stack` `📅 Week 1`

#### 1. 📌 What & Why
- **LIFO** (Last-In, First-Out) data structure
- In C: must manually define struct + functions (`push`, `pop`, `top`, `empty`) — error-prone, type-specific
- In C++: `std::stack<T>` from `<stack>` — template class, works for any type, well-tested
- Key C++ operations: `s.push(x)`, `s.pop()`, `s.top()`, `s.empty()`, `s.size()`

#### 2. 🔤 Syntax Reference
```cpp
#include <stack>
using namespace std;

stack<char> s;         // stack of chars — type specified in <>
stack<int>  si;        // stack of ints

s.push('A');           // add to top
s.top();               // peek at top — returns reference, does NOT remove
s.pop();               // remove top — returns void (does NOT return value)
s.empty();             // true if empty
s.size();              // number of elements
```
- **CRITICAL**: `s.pop()` returns **void** — you must call `s.top()` FIRST then `s.pop()`
- `s.top()` on empty stack = undefined behavior

#### 3. 💻 Code Example (Detailed)
```cpp
// Program 05.03 / 05.04 — Stack usage in C++
#include <iostream>
#include <cstring>
#include <stack>
using namespace std;

int main() {
    // Reverse a string using stack
    char str[10] = "ABCDE";
    stack<char> s;        // C++ stack — no initialization needed

    for (int i = 0; i < strlen(str); i++)
        s.push(str[i]);   // push each char

    cout << "Reversed String: ";
    while (!s.empty()) {
        cout << s.top();  // peek first
        s.pop();          // then remove
    }
    // Output: Reversed String: E D C B A
    return 0;
}
```

**🎯 NPTEL will ask:**
| # | Question | Answer | Why |
|---|----------|--------|-----|
| 1 | What does `s.pop()` return? | `void` — nothing | pop() only removes; use top() first |
| 2 | How do you get the top value of a C++ stack? | `s.top()` | top() returns reference, does not remove |
| 3 | What header is needed for `std::stack`? | `<stack>` | STL container adaptor |
| 4 | What is the underlying container for `std::stack` by default? | `deque` | Stack adapts deque by default |
| 5 | What happens with `push(&s, x)` vs `s.push(x)`? | First is C (struct pointer), second is C++ (object method) | Interface is cleaner in C++ |

#### 4. 📊 Comparison Table
| Aspect | C Stack | C++ `std::stack` |
|--------|---------|-----------------|
| Implementation | User-defined struct + functions | Built-in template class |
| Type-specific | Yes (must rewrite for each type) | No — `stack<T>` works for any `T` |
| Initialization | `s.top = -1;` needed | No initialization needed |
| push | `push(&s, x)` | `s.push(x)` |
| pop | `pop(&s)` | `s.pop()` (returns void) |
| top | `top(&s)` | `s.top()` (returns reference) |
| empty check | `empty(&s)` | `s.empty()` |
| Header | None (user code) | `<stack>` |

#### 5. ⚠️ Pitfalls
| Common Mistake | What Goes Wrong | Correct Approach |
|---------------|----------------|-----------------|
| `int x = s.pop()` | Compile error — pop() returns void | `int x = s.top(); s.pop();` |
| Calling `s.top()` on empty stack | Undefined behavior | Always check `!s.empty()` first |
| Forgetting `s.top = -1` in C stack | Stack appears non-empty | Always initialize C stack top to -1 |

#### 6. ⚡ Quick Recall
- `stack<T> s;` — no initialization needed
- `push(x)`, `top()` (peek), `pop()` (void!), `empty()`, `size()`
- **`pop()` returns void** — always call `top()` before `pop()`
- Default underlying container: `deque`
- C stack: struct + functions; C++ stack: template class in `<stack>`

---

<a name="topic-11"></a>
### 11. STL Containers Overview `📅 Week 1`

#### 1. 📌 What & Why
- C++ STL provides ready-made, type-safe, well-tested **container** classes
- Containers = class templates → work with any type
- Three main categories: Sequence, Associative, Unordered Associative
- Container Adaptors: `stack`, `queue`, `priority_queue` (built on top of sequence containers)

#### 2. 📊 Container Table

**Sequence Containers** (position-based access):
| Container | Class Template | Description |
|-----------|---------------|-------------|
| `array` [C++11] | Array class | 1D fixed-size array |
| `vector` | Vector | Resizable 1D array |
| `deque` | Double-ended queue | Expand/contract at both ends |
| `forward_list` [C++11] | Forward list | O(1) insert/erase, singly-linked |
| `list` | List | O(1) insert/erase anywhere, doubly-linked |

**Container Adaptors** (restricted interface):
| Container | Access Protocol | Default Underlying |
|-----------|----------------|-------------------|
| `stack` | LIFO | `deque` |
| `queue` | FIFO | `deque` |
| `priority_queue` | Priority | `vector` |

**Associative Containers** (key-based, typically BST):
| Container | Description |
|-----------|-------------|
| `set` | Unique elements, ordered |
| `multiset` | Multiple equivalent values, ordered |
| `map` | `<key, value>` pairs, unique keys, ordered |
| `multimap` | `<key, value>` pairs, duplicate keys, ordered |

**Unordered Associative Containers** [C++11] (hash-table based):
| Container | Description |
|-----------|-------------|
| `unordered_set` | Unique elements, no order (hash) |
| `unordered_multiset` | Multiple equivalents, no order |
| `unordered_map` | `<key, value>`, unique keys, no order |
| `unordered_multimap` | `<key, value>`, duplicate keys, no order |

**🎯 NPTEL will ask:**
| # | Question | Answer | Why |
|---|----------|--------|-----|
| 1 | Which containers are C++11 additions? | `array`, `forward_list`, all unordered_* | Tagged [C++11] in the spec |
| 2 | What is the default underlying container for `stack`? | `deque` | Stack adaptor wraps deque by default |
| 3 | What is the default underlying container for `priority_queue`? | `vector` | Priority queue adaptor wraps vector |
| 4 | How do `map` and `unordered_map` differ? | `map`: ordered (BST), `unordered_map`: no order (hash) | Different internal structures |
| 5 | What distinguishes `set` from `multiset`? | `set`: unique keys; `multiset`: allows duplicates | Multi prefix = allows duplicates |

#### 6. ⚡ Quick Recall
- `stack`/`queue`/`priority_queue` = **Container Adaptors** (not full containers)
- `stack` default: `deque`; `priority_queue` default: `vector`
- `array`, `forward_list`, `unordered_*` are **C++11** additions [C++11]
- `map` = ordered BST; `unordered_map` = hash table [C++11]
- All containers are **class templates** → work with any type

---

<a name="topic-12"></a>
### 12. C Preprocessor (CPP) — Macros, `#define`, `#undef` `📅 Week 1`

#### 1. 📌 What & Why
- CPP runs **before** compilation — does text substitution, not C++ syntax understanding
- `#define identifier replacement` — replaces every occurrence of `identifier` with `replacement`
- Function-like macros: `#define getmax(a,b) ((a)>(b)?(a):(b))`
- `#undef` removes a definition; `-D name` defines from command line; `-U name` undefines
- **No semicolons** at end of directives; backslash `\` continues to next line

#### 2. 🔤 Syntax Reference
```cpp
// Constant macro (manifest constant)
#define TABLE_SIZE 100
int arr[TABLE_SIZE];  // becomes: int arr[100];

// Function-like macro
#define getmax(a,b) ((a)>(b)?(a):(b))  // extra parens are CRITICAL
int y = getmax(x, 2);  // becomes: ((x)>(2)?(x):(2))

// # operator: stringize argument
#define str(x) #x
cout << str(test);  // becomes: cout << "test";

// ## operator: token paste / concatenate
#define glue(a,b) a ## b
glue(c,out) << "hello"; // becomes: cout << "hello";

// Undef and redefine
#define TABLE_SIZE 100
int table1[TABLE_SIZE];
#undef TABLE_SIZE
#define TABLE_SIZE 200
int table2[TABLE_SIZE];
// table1[100], table2[200]
```
- `#` (stringize): wraps argument in double quotes as a string literal
- `##` (token paste): concatenates two tokens
- Macros have **no block scope** — last until `#undef`

#### 3. 💻 Code Example (Detailed)
```cpp
// Function macro with all parentheses — CORRECT
#define getmax(a,b) ((a)>(b)?(a):(b))

// Example output
#include <iostream>
using namespace std;
int main() {
    int x = 5, y;
    y = getmax(x, 2);         // y = 5
    cout << y << endl;        // 5
    cout << getmax(7, x) << endl;  // 7
    return 0;
}
// Output:
// 5
// 7

// Command line compile:
// g++ Macros.cpp -D FLAG   →  FLAG is defined as 1
// g++ file.cpp -U FLAG     →  FLAG is undefined
```

**🎯 NPTEL will ask:**
| # | Question | Answer | Why |
|---|----------|--------|-----|
| 1 | What does `#define getmax(a,b) a>b?a:b` do vs `((a)>(b)?(a):(b))`? | Missing parens causes operator precedence bugs | e.g. `getmax(x+1, y)` without parens: `x+1>y?x+1:y` vs `(x+1)>(y)?(x+1):(y)` |
| 2 | What does `#x` do in a macro? | Converts `x` to a string literal | Stringize operator |
| 3 | What does `a ## b` do? | Concatenates tokens a and b | Token paste operator |
| 4 | What's the scope of a `#define`? | From definition to `#undef` or end of file | No block scope — not limited to `{}` |
| 5 | What does `-D FLAG` in `g++` do? | Defines `FLAG` as 1 | Command-line macro definition |

#### 5. ⚠️ Pitfalls
| Common Mistake | What Goes Wrong | Correct Approach |
|---------------|----------------|-----------------|
| `#define MAX(a,b) a>b?a:b` | Fails with expressions like `MAX(x+1, y)` | Always parenthesize: `((a)>(b)?(a):(b))` |
| Semicolon after `#define` | The semicolon becomes part of the replacement | No semicolons on `#define` |
| Using macros for constants in C++ | `const` is safer and type-checked | Prefer `const int MAX = 100;` in C++ |

#### 6. ⚡ Quick Recall
- CPP does **text substitution** before compilation — no type checking
- `#define X val` — constant; `#define F(a) (expr)` — function-like
- `#` = stringize; `##` = token paste
- `#undef X` removes the definition
- `-D name` from command line = `#define name 1`
- In C++: prefer `const` over `#define` for constants; prefer inline/templates over function macros

---

<a name="topic-13"></a>
### 13. Conditional Compilation — `#ifdef`, `#if`, `#ifndef` `📅 Week 1`

#### 1. 📌 What & Why
- Include or exclude code sections based on macro definitions — resolved at **preprocessor stage**
- `#ifdef`: include block if macro IS defined (regardless of value)
- `#ifndef`: include block if macro is NOT defined
- `#if expr`: include block if constant expression evaluates to non-zero
- `#elif` / `#else` / `#endif`: chaining conditions

#### 2. 🔤 Syntax Reference
```cpp
// ifdef: compile only if TABLE_SIZE is defined
#ifdef TABLE_SIZE
    int table[TABLE_SIZE];
#endif

// ifndef: define default if not defined
#ifndef TABLE_SIZE
    #define TABLE_SIZE 100
#endif
int table[TABLE_SIZE];  // uses 100 if not defined elsewhere

// if / elif / else / endif
#if TABLE_SIZE > 200
    #undef TABLE_SIZE
    #define TABLE_SIZE 200
#elif TABLE_SIZE < 50
    #undef TABLE_SIZE
    #define TABLE_SIZE 50
#else
    #undef TABLE_SIZE
    #define TABLE_SIZE 100
#endif
int table[TABLE_SIZE];

// defined() operator in #if
#if defined ARRAY_SIZE
    #define TABLE_SIZE ARRAY_SIZE
#elif !defined BUFFER_SIZE
    #define TABLE_SIZE 128
#else
    #define TABLE_SIZE BUFFER_SIZE
#endif
```

#### 3. 💻 Code Example (Detailed)
```cpp
// Use-Case 1: Comment out a block of code
#if 0                    // 0 = false → entire block excluded
    int debug_variable;
    cout << "This is never compiled";
#endif

// Use-Case 2: Debug builds
#ifdef _DEBUG
    cout << "Debug: value = " << x << endl;
#endif
// Build: g++ -g -D _DEBUG file.cpp    (debug build)
// Build: g++ file.cpp                  (release build)

// Use-Case 3: Platform control
#ifndef _BITS32
    // 64-bit code here
#else
    // 32-bit code here
#endif
// Build for 32-bit: g++ -D _BITS32 file.cpp
```

**🎯 NPTEL will ask:**
| # | Question | Answer | Why |
|---|----------|--------|-----|
| 1 | What does `#ifdef X` check? | Whether X is defined (value doesn't matter) | Even `#define X 0` makes `#ifdef X` true |
| 2 | What does `#if 0` do? | Excludes the block — equivalent to commenting it out | 0 is false; everything until `#endif` skipped |
| 3 | What is the difference between `#ifdef X` and `#if defined(X)`? | They are equivalent | Both check if X is defined |
| 4 | What ends a conditional compilation block? | `#endif` | Every `#if`/`#ifdef`/`#ifndef` must have a matching `#endif` |

#### 5. ⚠️ Pitfalls
| Common Mistake | What Goes Wrong | Correct Approach |
|---------------|----------------|-----------------|
| Missing `#endif` | Compile error | Every conditional block must be closed with `#endif` |
| `#ifdef X` where X is defined as 0 | Still TRUE — block is compiled | Use `#if X` to check value |
| Nesting `#if` without matching `#endif` | Compile error | Match every opening with a closing `#endif` |

#### 6. ⚡ Quick Recall
- `#ifdef X` — true if X is defined (ANY value, even 0)
- `#ifndef X` — true if X is NOT defined (classic include guard pattern)
- `#if expr` — evaluate constant expression
- `#if 0` — "comment out" a block of code
- `#ifdef _DEBUG` — standard pattern for debug-only code
- All conditional blocks MUST end with `#endif`

---

<a name="topic-14"></a>
### 14. `#include` Guards & Circular Inclusion `📅 Week 1`

#### 1. 📌 What & Why
- **Multiple Inclusion**: Same header included twice → duplicate definition → compile error
- **Circular Inclusion**: File A includes B, B includes A → infinite loop during preprocessing
- **`#include` Guard**: `#ifndef / #define / #endif` wrapper prevents multiple inclusion
- **`#pragma once`**: Modern alternative (non-standard but widely supported, GCC/MSVC)

#### 2. 🔤 Syntax Reference
```cpp
// Classic Include Guard (PORTABLE — works everywhere)
#ifndef __FILENAME_H
#define __FILENAME_H

// ... header content ...

#endif // __FILENAME_H

// Modern alternative (GCC, MSVC, Clang support it)
#pragma once
// ... header content ...
// No #endif needed — cleaner but may have portability issues
```
- Convention: guard macro = `__` + FILENAME_IN_UPPERCASE + `_H`
- First inclusion: `__FILENAME_H` undefined → enters block → defines it
- Second inclusion: `__FILENAME_H` already defined → skips entire file

#### 3. 💻 Code Example (Detailed)
```cpp
// File: grandparent.h
#ifndef GRANDPARENT_H    // first time: not defined → enter
#define GRANDPARENT_H    // now it's defined
struct foo { int member; };
#endif // GRANDPARENT_H

// File: parent.h
#ifndef PARENT_H
#define PARENT_H
#include "grandparent.h"  // grandparent.h included once, guarded
#endif // PARENT_H

// File: child.cpp
#include "grandparent.h"  // 1st include → enters guard, defines struct foo
#include "parent.h"       // parent.h includes grandparent.h again
                          // → GRANDPARENT_H is already defined → SKIPPED
// Result: struct foo defined ONCE ✅

// Without guard:
// struct foo { int member; };  ← twice → ERROR!
```

**🎯 NPTEL will ask:**
| # | Question | Answer | Why |
|---|----------|--------|-----|
| 1 | What problem does an `#include` guard solve? | Prevents multiple inclusion of the same header | Duplicate definitions cause compile errors |
| 2 | What is the guard check for `#ifndef __FOO_H` on second inclusion? | `__FOO_H` is already defined → block skipped | The define from first inclusion makes it skip |
| 3 | Can `#pragma once` replace `#ifndef` guards? | Yes, but may have portability issues | Not in C++ standard; most compilers support it |
| 4 | What is circular inclusion? | File A includes B, B includes A → infinite preprocessing loop | Guards prevent the infinite loop |

#### 5. ⚠️ Pitfalls
| Common Mistake | What Goes Wrong | Correct Approach |
|---------------|----------------|-----------------|
| No include guard in header | Multiple inclusion causes duplicate definitions | Always add `#ifndef / #define / #endif` |
| Guard macro name collision | Two different files with same guard name → one file skipped | Use unique names: `__FILENAME_H` convention |
| `#pragma once` without guard | May fail on some compilers/systems | Use classic guard or both |

#### 6. ⚡ Quick Recall
- Include guard = `#ifndef NAME` + `#define NAME` + code + `#endif`
- First inclusion: enters guard, defines macro
- Subsequent inclusions: macro defined → entire file skipped
- `#pragma once` = simpler alternative but less portable
- Circular inclusion: A → B → A → handled by guards (second inclusion skipped)

---

<a name="topic-15"></a>
### 15. Predefined Macros — `__LINE__`, `__FILE__`, `__cplusplus` `📅 Week 1`

#### 1. 📌 What & Why
- CPP provides built-in macros always available without `#define`
- Used for error reporting, debugging, version checking
- `__cplusplus` macro tells which C++ standard is being used — critical for version-dependent code
- These macros expand to useful info at **compile time**

#### 2. 🔤 Syntax Reference
```cpp
// Always-defined standard macros
__LINE__    // int: current line number in source file
__FILE__    // string: name of current source file (as a string literal)
__DATE__    // string: compilation date "Mmm dd yyyy"
__TIME__    // string: compilation time "hh:mm:ss"
__cplusplus // int: C++ standard version value

// Checking the C++ standard
if (__cplusplus == 201703L) // C++17
if (__cplusplus == 201402L) // C++14
if (__cplusplus == 201103L) // C++11
if (__cplusplus == 199711L) // C++98

// Checking C standard (C only)
__STDC_VERSION__            // long int
// 201710L = C18, 201112L = C11, 199901L = C99, 199409L = C89
```

#### 3. 💻 Code Example (Detailed)
```cpp
// Standard Macro Examples — from lecture
#include <iostream>
using namespace std;

int main() {
    cout << "This is the line number " << __LINE__;        // runtime value
    cout << " of file " << __FILE__ << ".\n";             // file name string
    cout << "Its compilation began " << __DATE__;
    cout << " at " << __TIME__ << ".\n";
    cout << "The compiler gives a __cplusplus value of " << __cplusplus;
    return 0;
}
// Sample output (actual values depend on compile):
// This is the line number 7 of file Macros.c.
// Its compilation began Sep 13 2021 at 11:30:07.
// The compiler gives a __cplusplus value of 201402
// (201402 = C++14)
```

**🎯 NPTEL will ask:**
| # | Question | Answer | Why |
|---|----------|--------|-----|
| 1 | What value does `__cplusplus` have for C++14? | `201402L` | Standard definition |
| 2 | What value does `__cplusplus` have for C++11? | `201103L` | Standard definition |
| 3 | What does `__LINE__` expand to? | Integer: current line number in source | CPP built-in |
| 4 | What format is `__DATE__`? | String literal `"Mmm dd yyyy"` | e.g., "Sep 13 2021" |
| 5 | What format is `__TIME__`? | String literal `"hh:mm:ss"` | e.g., "11:30:07" |

#### 4. 📊 Comparison Table
| Macro | Type | Value |
|-------|------|-------|
| `__LINE__` | `int` | Current source line number |
| `__FILE__` | `const char*` | Source filename string |
| `__DATE__` | `const char*` | "Mmm dd yyyy" |
| `__TIME__` | `const char*` | "hh:mm:ss" |
| `__cplusplus` | `long int` | 201703L/201402L/201103L/199711L |
| `__STDC_VERSION__` | `long int` | C standard version (C only) |

#### 5. ⚡ Quick Recall
- `__cplusplus`: C++17=`201703L`, C++14=`201402L`, C++11=`201103L`, C++98=`199711L`
- `__LINE__`: int; `__FILE__`, `__DATE__`, `__TIME__`: string literals
- These are predefined — no `#include` needed
- Used heavily in error reporting and version-conditional code

---

## 📦 Week Summary

| Concept | Module | Difficulty |
|---------|--------|-----------|
| C vs C++ I/O (`cout`, `cin`, `endl`) | M02 | 🟢 Easy |
| `namespace std` & Header Conventions | M02 | 🟢 Easy |
| Variable Declaration Scope (C89 vs C++) | M02 | 🟡 Medium |
| `bool` in C vs C++ | M02 | 🟢 Easy |
| Arrays vs `std::vector` | M03 | 🟡 Medium |
| C-strings vs `std::string` | M03 | 🟡 Medium |
| Sorting: `qsort` vs `std::sort` | M04 | 🟡 Medium |
| Searching: `bsearch` vs `binary_search` | M04 | 🟢 Easy |
| `<algorithm>` — `replace`, `rotate` | M04 | 🟡 Medium |
| Stack in C vs `std::stack` | M05 | 🟡 Medium |
| STL Containers Overview | M05 | 🔴 Hard |
| CPP Macros (`#define`, `#undef`, `#`, `##`) | T01 | 🔴 Hard |
| Conditional Compilation (`#ifdef`, `#if`) | T01 | 🟡 Medium |
| `#include` Guards & Circular Inclusion | T01 | 🟡 Medium |
| Predefined Macros (`__cplusplus`, etc.) | T01 | 🟡 Medium |

---

## 🎯 Practice MCQ / MSQ (NPTEL Style)

---

**Q1.** What is the output of the following C++ program?

```cpp
#include <iostream>
using namespace std;
int main() {
    double x = 2.0;
    cout << x << endl;
    return 0;
}
```
- (A) `2.000000`
- (B) `2.0`
- (C) `2`
- (D) `2.00000`

> ✅ Answer: **(C) `2`** — C++ `cout` default precision is 5 significant digits; trailing zeros after decimal are dropped. C's `printf("%lf", 2.0)` gives `2.000000`.

---

**Q2.** Which of the following is/are TRUE about `std::stack` in C++? *(MSQ)*

- (A) `pop()` removes the top element and returns it
- (B) `top()` peeks at the top element without removing it
- (C) The default underlying container is `deque`
- (D) It is defined in the `<stack>` header

> ✅ Answer: **(B), (C), (D)** — `pop()` returns `void`, not the element. `top()` only peeks. Default underlying container is `deque`. Header is `<stack>`.

---

**Q3.** What is the output of the following?

```cpp
#include <iostream>
#include <algorithm>
using namespace std;
int main() {
    int data[] = {1, 2, 3, 4, 5};
    rotate(data, data+2, data+5);
    for(int i = 0; i < 5; i++)
        cout << data[i] << " ";
}
```
- (A) `1 2 3 4 5`
- (B) `3 4 5 1 2`
- (C) `4 5 1 2 3`
- (D) `2 3 4 5 1`

> ✅ Answer: **(B) `3 4 5 1 2`** — `rotate(data, data+2, data+5)` makes `data[2]` (value `3`) the new first element; remaining elements follow in order, with `1,2` wrapping to the end.

---

**Q4.** Which of the following is the CORRECT C++ way to check if the compiler supports C++11?

- (A) `if (__cplusplus == 201103L)`
- (B) `if (__cplusplus == 199711L)`
- (C) `if (__STDC_VERSION__ == 201112L)`
- (D) `if (__cplusplus == 201402L)`

> ✅ Answer: **(A)** — `__cplusplus` value for C++11 is `201103L`. C++98 = `199711L`, C++14 = `201402L`. `__STDC_VERSION__` is for the C standard, not C++.

---

**Q5.** In C89, which of the following is INVALID?

```cpp
int main() {
    int a = 5;
    printf("%d", a);
    int b = 10;    // ← Line X
    return 0;
}
```
- (A) Declaring `a` and initializing it in the same line
- (B) Using `printf` before declaring `b`
- (C) Declaring `b` after a statement in C89
- (D) The `return 0` statement

> ✅ Answer: **(C)** — In C89/K&R, all variable declarations must appear at the **beginning of a block**, before any executable statements. Declaring `b` after `printf(...)` violates C89 rules. This is valid in C99 and C++.

---

**Q6.** What is the output of the following?

```cpp
#include <iostream>
using namespace std;
int main() {
    bool x = true;
    cout << "bool is " << x;
    return 0;
}
```
- (A) `bool is true`
- (B) `bool is 1`
- (C) `bool is True`
- (D) Compile error — `bool` needs `<stdbool.h>`

> ✅ Answer: **(B) `bool is 1`** — In C++, `bool` is a built-in type (no header needed). `cout` prints `bool` as `int` by default: `true` → `1`, `false` → `0`.

---

**Q7.** Which of the following are C++11 additions to the STL container library? *(MSQ)*

- (A) `vector`
- (B) `array`
- (C) `forward_list`
- (D) `unordered_map`
- (E) `stack`

> ✅ Answer: **(B), (C), (D)** — `array`, `forward_list`, and all `unordered_*` containers (`unordered_map`, `unordered_set`, etc.) were added in C++11. `vector` and `stack` existed before C++11.

---

**Q8.** What is the output of the following?

```cpp
#include <iostream>
#include <algorithm>
using namespace std;
int main() {
    int data[] = {1, 2, 3, 4, 5};
    replace(data, data+5, 3, 2);
    for(int i = 0; i < 5; i++)
        cout << data[i] << " ";
}
```
- (A) `1 2 3 4 5`
- (B) `1 2 2 4 5`
- (C) `1 2 3 2 5`
- (D) `2 2 2 4 5`

> ✅ Answer: **(B) `1 2 2 4 5`** — `replace(data, data+5, 3, 2)` replaces ALL occurrences of value `3` with value `2`. Only `data[2]` has value `3`, so result is `{1, 2, 2, 4, 5}`.

---

**Q9.** Consider the following C++ code. What does `#undef TABLE_SIZE` do?

```cpp
#define TABLE_SIZE 100
int table1[TABLE_SIZE];
#undef TABLE_SIZE
#define TABLE_SIZE 200
int table2[TABLE_SIZE];
```
- (A) Sets TABLE_SIZE to 0
- (B) Removes the definition of TABLE_SIZE so it can be redefined
- (C) Causes a compile error because TABLE_SIZE was already used
- (D) TABLE_SIZE remains 100 for all subsequent uses

> ✅ Answer: **(B)** — `#undef` removes the macro definition. After `#undef TABLE_SIZE`, the macro no longer exists and can be redefined with a new `#define`. `table1[100]` and `table2[200]` are the results.

---

**Q10.** Which of the following are TRUE about `#include` guards? *(MSQ)*

- (A) `#pragma once` is the standard C++ way to prevent multiple inclusion
- (B) `#ifndef / #define / #endif` is the portable way to prevent multiple inclusion
- (C) Without guards, including the same header twice causes a compile error for duplicate definitions
- (D) `#pragma once` is supported by GCC and MSVC but may have portability issues

> ✅ Answer: **(B), (C), (D)** — `#pragma once` is NOT in the C++ standard (A is false) but IS widely supported (D is true). The classic `#ifndef` guard IS portable (B). Without guards, duplicate struct/class definitions cause compile errors (C).

---
*Notes compiled for NPTEL exam preparation — Week 1 | Modules M01–M05, Tutorial T01*
