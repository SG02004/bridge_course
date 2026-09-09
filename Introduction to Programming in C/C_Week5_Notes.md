# Introduction to Programming in C — Week 5 Notes
### Prof. Satyadev Nandakumar, IIT Kanpur | Topic: Recursion

> ⚠️ Note: The uploaded transcript file was labeled "week5" and its content (Recursion — Linear, Linear-2, Two-way) matches **Week 5**, not Week 4. These notes are built for Week 5 accordingly.

---

## 📅 Week 5 — What is Recursion? (Base Case & Recursive Case)

### 1. Concept Summary
Recursion is when a function solves a problem by **calling itself** on a smaller version of the same problem. Every recursive function needs two parts: a **base case** (stops the recursion, solves directly) and a **recursive case** (does some work, then calls itself with smaller input). Without a correct, reachable base case → infinite recursion → **stack overflow**.

### 2. Key Syntax / Rules Box
```c
return_type function_name(parameters) {
    if (/* base condition */) {
        return /* direct answer, no further calls */;
    }
    // do some work with current input
    return function_name(/* smaller input */);   // recursive case
}
```
- The problem size **must strictly decrease** every call — otherwise infinite recursion.
- Base case must be **reachable** from every recursive path.
- Recursion ≈ Mathematical Induction: solve for base, assume it works for smaller n, build up.
- Each call gets its **own copy** of local variables/parameters (own stack frame).

### 3. Detailed Code Example — Linear Search (Recursive)
```c
int search(int a[], int n, int key) {
    if (n == 0) {
        return -1;              // Base case: empty array -> key not found
    }
    if (a[0] == key) {
        return 1;               // Found at current position
    }
    return search(a + 1, n - 1, key);  // Recursive case: shrink array by 1
}
```
**Why `a+1`?** Pointer arithmetic — `a+1` points to the next int, so the recursive call "sees" a smaller array starting one element later. `n-1` reflects the reduced size.

#### What would NPTEL ask about this?
- ❓ What happens if `n = 0` is never reached (e.g., function mistakenly called with `n-2` and n is odd, skipping 0)?
  ✅ Undefined behavior / crash (reads out of bounds) or infinite recursion → stack overflow.
  💡 Base case must exactly match how the size decreases each step.
- ❓ If `search(a, 5, key)` and key is at index 4, how many recursive calls (including the first) are made?
  ✅ 5 calls total (n=5,4,3,2,1... last call has n=1, checks a[0], found, returns 1).
  💡 Each call checks index 0 of the *current* sub-array, which maps to original index (5-n).
- ❓ What is returned if `key` is not present at all?
  ✅ -1, after n reaches 0.
  💡 Base case explicitly returns -1 only when array is exhausted.

### 4. Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|--------------|------------------|
| Forgetting base case | Infinite recursion → stack overflow (crash) | Always define `if (n==0) return ...;` first |
| Base case unreachable (wrong decrement, e.g. `n-2` on odd n) | Skips 0, keeps recursing into negative n | Match decrement to base-case check (or add `n<=0`) |
| Passing wrong pointer offset (`a` instead of `a+1`) | Infinite loop — array never shrinks | Always advance pointer along with reducing n |
| Recursive call result not returned/used | Function returns garbage even if recursion "worked" | Always `return function(...)` |

### 5. Quick Recall
- Recursion = function calling itself on a smaller sub-problem.
- Base case = stopping condition; Recursive case = work + smaller call.
- No base case (or unreachable) → stack overflow.
- Think of it like induction: solve n assuming n-1 (or smaller) is already solved.

---

## 📅 Week 5 — Linear Recursion (One Recursive Call Per Step)

### 1. Concept Summary
**Linear recursion** = function makes exactly **one** recursive call per invocation. It's the simplest recursion pattern — good for problems that reduce cleanly by a fixed amount each step (by 1, by 2, etc.). **Depth of recursion** = max stack size during execution = a key measure of memory usage (memory ∝ depth × per-call local storage).

### 2. Key Syntax / Rules Box
```c
// General linear recursion shape
T f(args) {
    if (base_condition) return base_value;
    // one recursive call:
    return combine(current_work, f(smaller_args));
}
```
- Stack depth ≈ ⌊(initial size) / (amount reduced per call)⌋ + 1.
- More stack space than an equivalent loop — trade code clarity for memory cost.
- "Minus infinity" convention: max of an **empty** array = very large negative number (so it never wins a comparison) — required to keep the recursive `max` logic correct for n=0.

### 3. Detailed Code Examples

**(a) In-place Array Reversal** — shrinks by 2 each call:
```c
void reverse(int *a, int n) {
    if (n == 0 || n == 1) {
        return;                      // Base case: 0 or 1 elements = already reversed
    }
    int temp = a[0];
    a[0] = a[n - 1];
    a[n - 1] = temp;                 // Swap first and last
    reverse(a + 1, n - 2);           // Recurse on inner sub-array (both ends excluded)
}
```
Stack depth ≈ `⌊n/2⌋ + 1` (matches n=7 example below: ⌊7/2⌋+1 = 4).

**(b) Maximum of an Array** — shrinks by 1 each call:
```c
int max_array(int *a, int n) {
    if (n == 0) {
        return -999999999;           // "minus infinity" convention for empty array
    }
    if (n == 1) {
        return a[0];                 // Base case: single element
    }
    int max_tail = max_array(a + 1, n - 1);   // Max of rest of array
    return (a[0] > max_tail) ? a[0] : max_tail;
}
```
Stack depth = `n` (much deeper than reversal — reduces by only 1 per call).

**(c) Euclidean GCD**:
```c
int gcd(int a, int b) {
    if (b == 0) {
        return a;                    // Base case
    }
    return gcd(b, a % b);            // Recursive case
}
```

#### What would NPTEL ask about this?
- ❓ For `reverse(a, 7)` (odd length, 7 elements), how many swaps happen and what's the recursion depth?
  ✅ 3 swaps (indices 0↔6, 1↔5, 2↔4); middle element (index 3) untouched. Depth = 4 calls (n=7,5,3,1).
  💡 Odd n reduces to n=1 base case eventually (not n=0); size drops by 2 each time.
- ❓ `max_array` called on an array of all negative numbers, e.g. `{-5,-3,-9}` — does the `-999999999` sentinel cause a bug?
  ✅ No — since -999999999 is smaller than any realistic negative test value, it never incorrectly "wins."
  💡 The sentinel only matters relative to comparisons; as long as it's smaller than all valid inputs it's safe (but it *would* break if actual input could be that negative — a common trap!).
- ❓ `gcd(0, 5)` — what is returned, and how many recursive calls?
  ✅ `gcd(0,5)` → b=5≠0 → `gcd(5, 0%5=0)` → b=0 → returns a=5. So GCD=5, 2 calls total.
  💡 Trace carefully: parameters swap roles each call (`gcd(b, a%b)`), don't assume a≥b always holds.
- ❓ Why does `max_array` have stack depth `n` but `reverse` has depth `~n/2`?
  ✅ `max_array` reduces size by 1/call; `reverse` reduces by 2/call.
  💡 Stack depth = (initial size) ÷ (reduction per call), roughly.

### 4. Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|--------------|------------------|
| Using `0` instead of large negative for empty-array max | Fails when all elements are negative | Use a sufficiently large negative sentinel (or handle n=0 as an error/special case) |
| Off-by-one in `reverse` (using `n-1` instead of `n-2` in recursive call) | Re-processes already-swapped elements or infinite loop | Always exclude both swapped elements: `reverse(a+1, n-2)` |
| Forgetting `n==1` as a separate base case in `max_array` | Extra unnecessary recursive call structure, or wrong result for empty vs single element | Handle `n==0` and `n==1` distinctly |
| Assuming linear recursion is always memory-cheap | Deep recursion (large n) can stack-overflow | Consider iterative or two-way recursion for large inputs |

### 5. Quick Recall
- Linear recursion = exactly one recursive call per step.
- Stack depth = size ÷ reduction-per-call (e.g., n for max_array, n/2 for reverse).
- Empty-array max uses "minus infinity" sentinel convention.
- GCD: `gcd(a,b) = a` if `b==0`, else `gcd(b, a%b)`.
- Recursive code is often shorter/clearer than iterative, but uses more stack memory.

---

## 📅 Week 5 — Two-way Recursion & Divide and Conquer

### 1. Concept Summary
**Two-way recursion**: a function makes **two** recursive calls per invocation, typically splitting the problem into two (roughly equal) halves — this is the **divide and conquer** strategy. For problems like array maximum, this drops stack depth from **O(n)** (linear recursion) to **O(log n)** — a huge efficiency win. But not all two-way recursive definitions are efficient (see Fibonacci below).

### 2. Key Syntax / Rules Box
```c
T f(args_of_size_n) {
    if (base_condition) return base_value;
    T left  = f(left_half);
    T right = f(right_half);
    return combine(left, right);
}
```
- Split sizes: left = `n/2`, right = `n - n/2` (handles odd `n` correctly — right half gets the extra element).
- Stack depth ≈ `1 + log₂(n)` for balanced halving (vs. `n` for linear recursion).
- Divide and conquer ≠ always efficient — depends on whether sub-problems overlap (see Fibonacci).

### 3. Detailed Code Example — Two-way Max Array
```c
int max_array(int *a, int n) {
    if (n == 0) {
        return -999999999;                       // MINUS_INFINITY, empty array
    }
    if (n == 1) {
        return a[0];                             // Single element
    }
    int left_max  = max_array(a, n / 2);          // Left half: n/2 elements
    int right_max = max_array(a + n / 2, n - n / 2); // Right half: remaining elements
    return (left_max > right_max) ? left_max : right_max;
}
```
For `n=1024`: linear recursion depth = 1024; two-way recursion depth ≈ `1 + log₂(1024) = 11`.

**Fibonacci — elegant but inefficient two-way recursion:**
```c
int fib(int n) {
    if (n == 0 || n == 1) {
        return 1;                    // Base cases: F0 = F1 = 1
    }
    return fib(n - 1) + fib(n - 2);  // Two recursive calls -> redundant work!
}
```
`fib(3)` gets computed twice inside `fib(5)`'s call tree, `fib(2)` three times, `fib(1)` five times — redundant computation grows **exponentially** with n (unlike the array-max case, where left/right halves never overlap).

#### What would NPTEL ask about this?
- ❓ What is the stack depth of `max_array(a, 100)` using two-way recursion?
  ✅ `1 + log₂(100) ≈ 1 + 6.64 → 7` (ceiling), i.e., ~7–8.
  💡 Depth = ceil(log₂ n) + 1 for halving recursion; always round appropriately since n isn't a power of 2.
- ❓ Why is two-way recursion efficient for `max_array` but inefficient for `fib`?
  ✅ In `max_array`, left and right halves are **disjoint** (no overlap/re-computation). In `fib`, `fib(n-1)` and `fib(n-2)` calls **overlap** heavily (both eventually recompute the same smaller Fibonacci values).
  💡 Two-way recursion's efficiency depends on whether sub-problems share work, not just on the branching itself.
- ❓ How many total calls does `fib(4)` make (including itself)?
  ✅ 9 calls: fib(4)→fib(3)+fib(2); fib(3)→fib(2)+fib(1); each fib(2)→fib(1)+fib(0). Full tree: fib(4),fib(3),fib(2),fib(1),fib(0),fib(2),fib(1),fib(0),fib(1) = 9.
  💡 Draw the call tree; count nodes, don't just guess — exponential growth is easy to underestimate.
- ❓ In two-way `max_array`, what if the split was `n/2` and `n/2` (both floor, not `n - n/2` for the right half) for odd n?
  ✅ Bug: one element would be dropped/lost from the array (never visited).
  💡 Right half MUST be `n - n/2` to account for the "extra" element when n is odd.

### 4. Common Pitfalls Table
| Mistake | What happens | Correct version |
|---------|--------------|------------------|
| Using `n/2` for both halves | Loses the last element when n is odd | Right half size = `n - n/2` |
| Wrong pointer offset for right half (e.g. `a + n/2 + 1`) | Skips or duplicates an element | Right half starts at `a + n/2` exactly |
| Assuming all two-way recursion is O(log n) fast | Naive Fibonacci is exponential time despite two calls | Check for overlapping sub-problems; use memoization if needed |
| Forgetting both base cases (`n=0` and `n=1`) | Infinite recursion or wrong answer for small arrays | Always handle n=0 and n=1 explicitly |

### 5. Quick Recall
- Two-way recursion = 2 recursive calls per step (divide & conquer).
- Balanced array split: left = `n/2`, right = `n - n/2`.
- Stack depth for halving recursion ≈ `1 + log₂n` (vs. `n` for linear).
- Fibonacci: elegant two-way recursion but exponential time due to **redundant/overlapping** sub-calls — efficiency of two-way recursion depends on whether sub-problems overlap.

---

## 🧪 Weekly Assignment Analysis (Assignment 5)

### Question 1 — Collatz Sequence Steps
**Problem:** Given `n`, count how many times `f` must be applied to first reach 1, where `f(n) = 3n+1` (odd) or `n/2` (even).

**Solution:**
```c
int collatz_repeat(int n) {
    if (n == 1) {
        return 0;
    } else {
        if (n % 2 == 1) {
            return 1 + collatz_repeat(3 * n + 1);
        } else {
            return 1 + collatz_repeat(n / 2);
        }
    }
}
```
**Why this is correct:**
- **Base case:** `n == 1` → 0 more steps needed. This correctly stops recursion since the Collatz sequence is defined to terminate at 1.
- **Recursive case:** Applies `f` once (odd → `3n+1`, even → `n/2`), adds 1 to the count, and recurses on the *result* — mirroring the problem definition exactly (linear recursion, one call per step).
- Matches the worked example: for `n=7`, the recursion unwinds to give 16 — the given answer.
- **Why not use a loop instead of recursion here?** Both work, but recursion directly mirrors "apply f, then count how many more applications are needed on the result" — a natural fit for linear recursion (this week's theme). An iterative version would use a `while` loop with a counter, functionally equivalent.
- **Common wrong answers to watch for:** Forgetting to add 1 in the recursive call → undercounts. Using `n <= 1` as base case → works too since Collatz never reaches ≤0, but `n==1` is the precise/intended condition.

---

### Question 2 — Generate All Binary Strings of Length N
**Problem:** Recursively generate and print all binary (0/1) strings of length `N`, in lexicographic order.

**Solution:**
```c
void genBinary(char *s, int i, int N) {
    if (i == N) {
        s[N] = '\0';
        printf("%s\n", s);
        return;
    }
    s[i] = '0';
    genBinary(s, i + 1, N);
    s[i] = '1';
    genBinary(s, i + 1, N);
}
```
**Why this is correct:**
- **Base case:** `i == N` means all `N` positions have been filled → terminate the string with `'\0'` and print it.
- **Recursive case (two-way recursion):** At each position `i`, try `'0'` first (explore that entire branch fully — all combinations with `0` at position `i`), then try `'1'` (explore that branch). This ordering guarantees **lexicographic order** because `'0'` sorts before `'1'`, and each branch completes before the next begins (depth-first).
- This is a **tree recursion** (branching factor 2 at each of N levels) — similar in shape to two-way recursion but here both calls happen unconditionally (not divide-and-conquer on data, but exploring choices).
- **Why is this two-way, not linear?** Two calls (`'0'` branch, `'1'` branch) happen at *every* position — total leaf calls = 2^N, matching all binary strings of length N.
- **Common wrong answers to watch for:** Swapping the order (`'1'` before `'0'`) → reverses lexicographic order. Forgetting `s[N]='\0'` → `printf("%s")` reads garbage past the buffer (undefined behavior). Off-by-one in array size (`char A[8]` only safely supports N up to 7, since index N needs the null terminator — for N=8 this would overflow; the constraint `0<N<10` combined with `A[8]` is a subtle mismatch to note, though typical test cases likely stay within safe bounds).

---

### Question 3 — Merge Two Sorted Arrays
**Problem:** Merge two sorted arrays of size `N` and `M` into one sorted array of size `N+M`.

**Solution (iterative, not recursive):**
```c
int main() {
    int n, m;
    scanf("%d %d", &n, &m);
    int a[n], b[m], c[n + m];

    for (int i = 0; i < n; i++) scanf("%d", &a[i]);
    for (int i = 0; i < m; i++) scanf("%d", &b[i]);

    int i = 0, j = 0, k = 0;
    while (i < n && j < m) {
        if (a[i] < b[j]) c[k++] = a[i++];
        else              c[k++] = b[j++];
    }
    while (i < n) c[k++] = a[i++];   // leftover elements from a
    while (j < m) c[k++] = b[j++];   // leftover elements from b

    for (i = 0; i < n + m; i++) printf("%d ", c[i]);
    return 0;
}
```
**Why this is correct:**
- **Main merge loop:** Compares current unmerged elements of `a` and `b`; always picks the smaller, advances that array's index, and writes into `c`. Since both `a` and `b` are individually sorted, this greedy comparison always places the globally next-smallest element into `c`.
- **Two cleanup loops:** Once one array is exhausted, the *other* array's remaining elements are already sorted relative to each other and all larger than everything placed so far — so they can just be copied directly (no more comparisons needed).
- **Why `a[i] < b[j]` and not `<=`?** Using `<=` instead would still be correct for merge stability/order (equal elements would just come from `a` first) — either works for producing a correctly *sorted* output; this is a common "trap" where students think there's a bug when actually both comparisons are valid, only affecting which array's duplicate is picked first.
- **Common wrong answers to watch for:** Forgetting either cleanup `while` loop → loses trailing elements from whichever array wasn't exhausted first. Using `i <= n` (off-by-one) in loops → reads out of bounds. Declaring `c[n+m]` before reading `n`, `m` → invalid (variable-length arrays must be declared after their size is known, as done correctly here).

---

## 📋 Exam-Day Summary Cheat Sheet

| Pattern | Recursive calls/step | Typical stack depth | Example |
|---|---|---|---|
| Linear recursion | 1 | O(n) or O(n/2) | search, reverse, max_array, gcd |
| Two-way recursion (divide & conquer, disjoint) | 2 | O(log n) | two-way max_array |
| Two-way recursion (overlapping) | 2 | O(n) depth, but O(2ⁿ) total calls | naive fibonacci |
| Tree recursion (all choices) | 2 (or more) at every level | O(N) depth, O(2^N) leaves | genBinary |

**Golden rules to check on any recursive code MCQ:**
1. Is there a base case? Is it reachable?
2. Does the problem size strictly shrink toward the base case?
3. Trace 2–3 small examples by hand (n=0,1,2,3) before trusting your intuition.
4. For two-way recursion: do the two calls overlap (redundant work) or not?
