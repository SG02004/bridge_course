# Introduction to Programming in C — Week 5 Notes
### Prof. Satyadev Nandakumar, IIT Kanpur | Topic: Recursion

> ⚠️ Note: The uploaded transcript file was labeled "week5" and its content (Recursion — Linear, Linear-2, Two-way) matches **Week 5**, not Week 4. These notes are built for Week 5 accordingly.

---

## 📅 Week 5 — What is Recursion? (Base Case & Recursive Case)

### 1. Concept Summary

Recursion is a programming technique where a function **solves a problem by calling itself** — but on a *smaller* version of that same problem. Think of it like peeling an onion: each call peels one layer, and at some point you reach the core (the **base case**), where there is nothing left to peel and you stop.

Every correct recursive function must have **two parts**:
- **Base case**: The smallest version of the problem that can be answered directly — no further calls needed. This is what *stops* the recursion.
- **Recursive case**: The function does some work on the *current* input, then calls *itself* with a *strictly smaller* input — moving one step closer to the base case.

The key word above is **strictly smaller**. If the recursive call doesn't make the input smaller every time, the function never reaches the base case — and it calls itself forever, filling up the program's call stack until the computer crashes with a **stack overflow** error.

A useful mental model: recursion works exactly like **mathematical induction**. To prove a statement holds for all n, you prove it for the base (n=0 or n=1), and then prove that IF it holds for n-1 (or smaller), it must also hold for n. The recursive function does the same: it *assumes* the recursive call will correctly solve the smaller problem, then uses that result to solve the current one.

Each time a function calls itself, C creates a **new stack frame** — a fresh copy of all local variables and parameters — for that call. The frames pile up while recursion goes deeper, and are popped off one by one as each call returns. This is why deep recursion uses a lot of memory.

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

**The idea:** Search for `key` in array `a[]` of size `n`. Check the first element; if it matches, we're done. Otherwise, search the rest of the array (everything from index 1 onward).

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

**Line-by-line explanation:**

| Line | What it does |
|------|-------------|
| `if (n == 0) return -1;` | Base case: if there are no elements left to check, the key was never found. Return -1. |
| `if (a[0] == key) return 1;` | Check the *current first element*. If it matches, key is found — return 1. |
| `return search(a + 1, n - 1, key);` | Key wasn't at position 0. Move to the next sub-array: `a+1` skips the first element (pointer arithmetic), `n-1` reflects one fewer element. |

**Why `a+1`?** In C, arrays are accessed via pointers. `a` points to the first element. `a+1` points to the *second* element. So passing `a+1` with size `n-1` makes the recursive call "see" the array starting from the second element — effectively shrinking the array from the left by one element each call.

**Concrete trace — searching for key=3 in `{5, 2, 3, 8}` (n=4):**

```
search({5,2,3,8}, 4, 3)
  n=4, a[0]=5 ≠ 3  →  search({2,3,8}, 3, 3)
    n=3, a[0]=2 ≠ 3  →  search({3,8}, 2, 3)
      n=2, a[0]=3 == 3  →  return 1  ✅
    returns 1
  returns 1
returns 1
```

**Trace when key is not found — searching for 9 in `{5, 2}` (n=2):**
```
search({5,2}, 2, 9)
  n=2, a[0]=5 ≠ 9  →  search({2}, 1, 9)
    n=1, a[0]=2 ≠ 9  →  search({}, 0, 9)
      n=0  →  return -1  ✅
    returns -1
  returns -1
returns -1
```

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

### 4. Quick Recall
- Recursion = function calling itself on a smaller sub-problem.
- Base case = stopping condition; Recursive case = work + smaller call.
- No base case (or unreachable) → stack overflow.
- Think of it like induction: solve n assuming n-1 (or smaller) is already solved.

---

## 📅 Week 5 — Linear Recursion (One Recursive Call Per Step)

### 1. Concept Summary

**Linear recursion** is the simplest form of recursion: every function invocation makes **exactly one** recursive call. There is no branching — the recursion goes in a straight line, like a chain. One call leads to one call leads to one call, until the base case is hit, and then all the return values unwind back up the chain.

This "straight-line" structure is why we say it's *linear* — just as a linked list has one node pointing to the next, a linearly recursive function has one call pointing to the next smaller call.

Problems that reduce naturally by a fixed amount at each step — "look at one element, then handle the rest" — are a perfect fit for linear recursion. Array search, reversal, finding a maximum, and Euclid's GCD algorithm all fit this mold.

The main cost of linear recursion is **memory**. Each recursive call creates a new stack frame. If the problem has size `n` and reduces by 1 each call, the call stack grows to depth `n` before unwinding. If it reduces by 2 each call, depth is roughly `n/2`. The general rule:

> **Stack depth ≈ (initial size) ÷ (reduction per call)**

For large `n`, this can be significant. An iterative loop with the same logic uses O(1) memory (no growing stack). Recursive code is often more elegant and easier to reason about, but it costs stack space — and for very large inputs, it can crash with a stack overflow that a loop would never cause.

The "minus infinity" sentinel is an important convention that comes up with maximum-finding: when we ask "what is the maximum of an *empty* array?", there is no sensible numerical answer. By convention, we return a very large negative number (conceptually −∞). This ensures that when we compare it against any real array element, the real element will always "win" — so the sentinel never corrupts the result.

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

---

**(a) In-place Array Reversal** — shrinks by 2 each call

**The idea:** Swap the first and last elements, then recursively reverse everything in between (the inner sub-array).

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

**Line-by-line explanation:**

| Line | What it does |
|------|-------------|
| `if (n == 0 \|\| n == 1) return;` | Base case: an array of 0 or 1 elements is trivially already reversed — nothing to do. |
| `temp = a[0]; a[0] = a[n-1]; a[n-1] = temp;` | Classic 3-variable swap. Exchanges the outermost two elements. |
| `reverse(a + 1, n - 2);` | The outermost elements are handled. Now reverse the *inner* portion: skip the first (`a+1`) and exclude the last (`n-2` instead of `n`). |

**Why `n-2` and not `n-1`?** We already handled *both* the first and last elements (swapped them). So the inner sub-array has 2 fewer elements than the current array — hence `n-2`.

**Concrete trace — `reverse({1,2,3,4,5}, 5)`:**
```
reverse({1,2,3,4,5}, 5)  →  swap 1↔5  →  {5,2,3,4,1}
  reverse({2,3,4}, 3)    →  swap 2↔4  →  {5,4,3,2,1}
    reverse({3}, 1)       →  n==1, return  ✅
```
Stack depth = 3 calls (n = 5, 3, 1). The middle element (3) stays in place automatically.

**Trace for even n — `reverse({1,2,3,4}, 4)`:**
```
reverse({1,2,3,4}, 4)  →  swap 1↔4  →  {4,2,3,1}
  reverse({2,3}, 2)    →  swap 2↔3  →  {4,3,2,1}
    reverse({}, 0)      →  n==0, return  ✅
```
Stack depth = 3 calls (n = 4, 2, 0). Both base cases (`n==0` and `n==1`) are needed!

Stack depth formula: ≈ `⌊n/2⌋ + 1`. For n=5: ⌊5/2⌋+1 = 3. For n=7: ⌊7/2⌋+1 = 4. ✅

---

**(b) Maximum of an Array** — shrinks by 1 each call

**The idea:** The maximum of an array is either the first element, or the maximum of the rest. Compare those two.

```c
int max_array(int *a, int n) {
    if (n == 0) {
        return -999999999;           // "minus infinity" convention for empty array
    }
    if (n == 1) {
        return a[0];                 // Base case: single element is the max
    }
    int max_tail = max_array(a + 1, n - 1);   // Max of rest of array
    return (a[0] > max_tail) ? a[0] : max_tail;
}
```

**Line-by-line explanation:**

| Line | What it does |
|------|-------------|
| `if (n == 0) return -999999999;` | Empty array — no maximum exists. Return "minus infinity" (a sentinel so small no real value loses to it). |
| `if (n == 1) return a[0];` | One element — that element *is* the maximum. Return it. |
| `max_tail = max_array(a+1, n-1);` | Recursively find the maximum of everything *except* the first element. |
| `return (a[0] > max_tail) ? a[0] : max_tail;` | The overall max is whichever is bigger: the first element, or the max of the rest. |

**Concrete trace — `max_array({3, 7, 2, 9, 1}, 5)`:**
```
max_array({3,7,2,9,1}, 5)
  max_tail = max_array({7,2,9,1}, 4)
    max_tail = max_array({2,9,1}, 3)
      max_tail = max_array({9,1}, 2)
        max_tail = max_array({1}, 1)  →  return 1
        return (9 > 1) ? 9 : 1  =  9
      return (2 > 9) ? 2 : 9   =  9
    return (7 > 9) ? 7 : 9     =  9
  return (3 > 9) ? 3 : 9       =  9  ✅
```
Stack depth = 5 (n = 5, 4, 3, 2, 1) — every call reduces n by just 1, so depth equals n.

**Why two base cases (n==0 and n==1)?** The `n==0` case handles when we call on an empty slice and returns the sentinel. The `n==1` case is the "real" stopping point — there's only one element, so it's trivially the max. Without `n==1`, the function would recurse to n==0 and return the sentinel instead of the last real element, then compare the last element against -999999999 — this still works, but having both makes the logic cleaner and avoids that extra unnecessary call.

---

**(c) Euclidean GCD:**

**The idea:** `gcd(a, b) = gcd(b, a % b)` because any common divisor of a and b also divides `a % b`. When the remainder becomes 0, `a` itself is the GCD.

```c
int gcd(int a, int b) {
    if (b == 0) {
        return a;                    // Base case: gcd(a, 0) = a
    }
    return gcd(b, a % b);            // Recursive case: gcd(a,b) = gcd(b, a mod b)
}
```

**Concrete trace — `gcd(48, 18)`:**
```
gcd(48, 18)  →  b=18≠0  →  gcd(18, 48%18=12)
  gcd(18, 12)  →  b=12≠0  →  gcd(12, 18%12=6)
    gcd(12, 6)  →  b=6≠0   →  gcd(6, 12%6=0)
      gcd(6, 0)  →  b==0  →  return 6  ✅
```

**Concrete trace — `gcd(0, 5)`:**
```
gcd(0, 5)  →  b=5≠0  →  gcd(5, 0%5=0)
  gcd(5, 0)  →  b==0  →  return 5  ✅
```
Note: parameters *swap roles* each call. Don't assume a ≥ b — `gcd(3, 7)` works fine: `gcd(7, 3%7... wait: 3%7=3)` — actually: `gcd(3,7)→gcd(7,3%7=3)→gcd(3,7%3=1)→gcd(1,0)→1`. It self-corrects.

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

### 4. Quick Recall
- Linear recursion = exactly one recursive call per step.
- Stack depth = size ÷ reduction-per-call (e.g., n for max_array, n/2 for reverse).
- Empty-array max uses "minus infinity" sentinel convention.
- GCD: `gcd(a,b) = a` if `b==0`, else `gcd(b, a%b)`.
- Recursive code is often shorter/clearer than iterative, but uses more stack memory.

---

## 📅 Week 5 — Two-way Recursion & Divide and Conquer

### 1. Concept Summary

**Two-way recursion** is when each function call makes **two** recursive calls instead of one. The pattern looks like a branching tree rather than a straight chain.

The most powerful use of two-way recursion is **divide and conquer**: split the problem into two roughly equal halves, solve each half independently, then combine the results. The magic of this approach is in the stack depth. With linear recursion, if we process one element per call, the stack goes n levels deep. With divide-and-conquer, each call halves the size — so after just ~log₂(n) levels we've reached the base case. For n=1024, that's a stack depth of 10 instead of 1024. This is a massive win.

But two-way recursion is not *automatically* efficient. The crucial question is: **do the two sub-calls overlap?** That is, do they end up solving the same smaller problem?

- In **divide-and-conquer max_array**, the left half and right half are completely disjoint — they look at different array elements. No work is repeated. This is efficient.
- In **naive Fibonacci**, `fib(n)` calls `fib(n-1)` and `fib(n-2)`. But `fib(n-1)` internally also calls `fib(n-2)`. And both of those call `fib(n-3)`. The same values are recomputed again and again, exponentially. For `fib(50)`, this means billions of redundant calls — hopelessly slow.

So the rule is: two-way recursion gives you O(log n) stack depth, but only gives you *efficient total computation* when the two sub-problems don't share work.

**Tree recursion** (seen in binary string generation) is similar — two calls at every level — but the goal is to *explore all possibilities* (all choices at each position), not divide a fixed-size input. The stack depth is still O(N), and the total calls is 2^N (one leaf per combination).

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

### 3. Detailed Code Examples

---

**(a) Two-way Max Array — Divide and Conquer**

**The idea:** Split the array in half. Find the max of the left half (recursively). Find the max of the right half (recursively). Return whichever is larger.

```c
int max_array(int *a, int n) {
    if (n == 0) {
        return -999999999;                          // MINUS_INFINITY, empty array
    }
    if (n == 1) {
        return a[0];                                // Single element
    }
    int left_max  = max_array(a, n / 2);            // Left half: first n/2 elements
    int right_max = max_array(a + n/2, n - n/2);   // Right half: remaining elements
    return (left_max > right_max) ? left_max : right_max;
}
```

**Line-by-line explanation:**

| Line | What it does |
|------|-------------|
| `if (n == 0) return -999999999;` | Empty array → return minus-infinity sentinel (same as before). |
| `if (n == 1) return a[0];` | Single element → it IS the max. Base case stops recursion. |
| `left_max = max_array(a, n/2);` | Recurse on the left half. `a` (unchanged pointer) + `n/2` elements. |
| `right_max = max_array(a + n/2, n - n/2);` | Recurse on the right half. Pointer advances by `n/2` elements; size is `n - n/2` (handles odd n correctly). |
| `return (left_max > right_max) ? ... ;` | Overall max is whichever half's max is bigger. |

**Why `n - n/2` and NOT `n/2` for the right half?**
When `n` is odd (say n=5): `n/2 = 2` (integer division). Left half gets 2 elements. Right half must get `5-2 = 3` elements. If we mistakenly wrote `n/2` for both, we'd get 2+2=4 elements processed, missing one entirely — a silent bug.

**Concrete trace — `max_array({3,7,2,9,1}, 5)`:**
```
max_array({3,7,2,9,1}, 5)
  left  = max_array({3,7}, 2)
            left  = max_array({3}, 1)  →  return 3
            right = max_array({7}, 1)  →  return 7
            return max(3,7) = 7
  right = max_array({2,9,1}, 3)
            left  = max_array({2}, 1)     →  return 2
            right = max_array({9,1}, 2)
                      left  = max_array({9},1)  →  return 9
                      right = max_array({1},1)  →  return 1
                      return max(9,1) = 9
            return max(2,9) = 9
  return max(7,9) = 9  ✅
```

**Stack depth comparison (n=1024):**
```
Linear recursion:  depth = 1024  (one element peeled per call)
Two-way recursion: depth = 1 + log₂(1024) = 1 + 10 = 11  ✅
```

---

**(b) Fibonacci — Elegant but Inefficient Two-Way Recursion**

**The idea:** F(0)=1, F(1)=1, F(n) = F(n-1) + F(n-2). Natural recursive definition.

```c
int fib(int n) {
    if (n == 0 || n == 1) {
        return 1;                     // Base cases: F(0) = F(1) = 1
    }
    return fib(n - 1) + fib(n - 2);  // Two recursive calls → redundant work!
}
```

**Call tree for `fib(5)` — showing repeated work:**
```
                    fib(5)
                  /        \
            fib(4)          fib(3)
           /      \        /      \
       fib(3)   fib(2)  fib(2)  fib(1)
       /    \   /    \   /    \
   fib(2) fib(1) fib(1) fib(0) fib(1) fib(0)
   /    \
fib(1) fib(0)
```

**fib(3) is computed TWICE. fib(2) is computed THREE times. fib(1) appears FIVE times.**

For `fib(4)`: total calls = 9 (count all nodes in the tree above, trimmed to fib(4)).
For `fib(5)`: total calls = 15.
For `fib(n)`: total calls grows roughly as **2^n** — exponentially.

This is fundamentally different from `max_array`: there, left and right halves covered *different* array elements, so no work was shared. Here, `fib(n-1)` and `fib(n-2)` both eventually recurse down to the same `fib(2)`, `fib(1)`, `fib(0)` — repeating massive amounts of computation.

**How many total calls does `fib(4)` make?**
```
fib(4) calls fib(3) and fib(2)
fib(3) calls fib(2) and fib(1)
fib(2) calls fib(1) and fib(0)  → (appears twice above, so counted twice)
fib(1) and fib(0) are base cases
Total: fib(4), fib(3), fib(2)×2, fib(2)×1(from fib(3)), fib(1)×3, fib(0)×2 = 9 calls
```

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

### 4. Quick Recall
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

**Line-by-line explanation:**

| Line | What it does |
|------|-------------|
| `if (n == 1) return 0;` | Base case: we're already at 1. Zero more steps needed. |
| `if (n % 2 == 1)` | Check if n is odd. In C, `%` gives the remainder; if it's 1, n is odd. |
| `return 1 + collatz_repeat(3*n+1);` | Apply the Collatz odd rule: n → 3n+1. Add 1 (for this step), recurse on the result. |
| `return 1 + collatz_repeat(n/2);` | Apply the Collatz even rule: n → n/2. Add 1 (for this step), recurse on the result. |

**Concrete trace — `collatz_repeat(6)`:**
```
collatz_repeat(6)   → 6 is even → 1 + collatz_repeat(3)
  collatz_repeat(3) → 3 is odd  → 1 + collatz_repeat(10)
    collatz_repeat(10) → 10 is even → 1 + collatz_repeat(5)
      collatz_repeat(5) → 5 is odd  → 1 + collatz_repeat(16)
        collatz_repeat(16) → even → 1 + collatz_repeat(8)
          collatz_repeat(8) → even → 1 + collatz_repeat(4)
            collatz_repeat(4) → even → 1 + collatz_repeat(2)
              collatz_repeat(2) → even → 1 + collatz_repeat(1)
                collatz_repeat(1) → return 0
              return 1+0 = 1
            return 1+1 = 2
          return 1+2 = 3
        return 1+3 = 4
      return 1+4 = 5
    return 1+5 = 6
  return 1+6 = 7
return 1+7 = 8
```
Sequence: 6 → 3 → 10 → 5 → 16 → 8 → 4 → 2 → 1. **8 steps.** ✅

**Why this is correct:**
- Base case `n==1` exactly matches termination — Collatz always eventually reaches 1 (assumed for NPTEL purposes).
- Each branch applies the correct rule and adds 1 for the step just taken.
- This is linear recursion: exactly one recursive call per invocation (one branch is always skipped by the if/else).

**Common wrong answers to watch for:** Forgetting `+1` in the recursive call → always returns 0. Using `n <= 1` as base case → also works (Collatz never goes below 1), but `n==1` is the precise condition.

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
    genBinary(s, i + 1, N);   // Explore all strings that start with '0' at position i
    s[i] = '1';
    genBinary(s, i + 1, N);   // Explore all strings that start with '1' at position i
}
```

**Line-by-line explanation:**

| Line | What it does |
|------|-------------|
| `if (i == N)` | Base case: we've filled all N positions (indices 0 to N-1). |
| `s[N] = '\0';` | Null-terminate the string so `printf("%s")` knows where it ends. |
| `printf("%s\n", s);` | Print the complete binary string. |
| `s[i] = '0'; genBinary(s, i+1, N);` | Put '0' at current position, then recursively fill the rest. This entire subtree (all strings with '0' here) is explored before we move on. |
| `s[i] = '1'; genBinary(s, i+1, N);` | After all '0' strings are printed, put '1' at current position and explore that subtree. |

**Why does this produce lexicographic order?** Because `'0' < '1'` in ASCII, placing '0' first and fully exploring that branch before placing '1' means we always print smaller strings first — exactly lexicographic order. This is a depth-first traversal of a binary tree.

**Concrete trace — `genBinary(s, 0, 2)` (all 2-bit strings):**
```
i=0: s[0]='0' → recurse i=1
  i=1: s[1]='0' → recurse i=2
    i==N=2: print "00"
  i=1: s[1]='1' → recurse i=2
    i==N=2: print "01"
i=0: s[0]='1' → recurse i=1
  i=1: s[1]='0' → recurse i=2
    i==N=2: print "10"
  i=1: s[1]='1' → recurse i=2
    i==N=2: print "11"

Output: 00, 01, 10, 11  ✅
```

**Why is this two-way recursion?** Two calls at every non-base-case invocation (one for '0', one for '1'). Stack depth = N (filling one position per level). Total leaf calls = 2^N = total binary strings.

**Common wrong answers to watch for:** Swapping `'0'` and `'1'` order → reverses to 11,10,01,00. Forgetting `s[N]='\0'` → `printf` reads garbage past the buffer. Using `char A[N]` instead of `char A[N+1]` → no room for the null terminator.

---

### Question 3 — Merge Two Sorted Arrays

**Problem:** Merge two sorted arrays of size `N` and `M` into one sorted array of size `N+M`.

**Solution (iterative):**
```c
int main() {
    int n, m;
    scanf("%d %d", &n, &m);
    int a[n], b[m], c[n + m];

    for (int i = 0; i < n; i++) scanf("%d", &a[i]);
    for (int i = 0; i < m; i++) scanf("%d", &b[i]);

    int i = 0, j = 0, k = 0;
    while (i < n && j < m) {
        if (a[i] < b[j]) c[k++] = a[i++];   // a's current element is smaller
        else              c[k++] = b[j++];    // b's current element is smaller or equal
    }
    while (i < n) c[k++] = a[i++];   // leftover elements from a
    while (j < m) c[k++] = b[j++];   // leftover elements from b

    for (i = 0; i < n + m; i++) printf("%d ", c[i]);
    return 0;
}
```

**Line-by-line explanation:**

| Section | What it does |
|---------|-------------|
| `scanf` block | Read n, m, then the elements of a[] and b[]. |
| `i=0, j=0, k=0` | Three pointers: `i` tracks position in `a`, `j` tracks position in `b`, `k` tracks where to write in `c`. |
| Main `while (i<n && j<m)` | Keep going as long as BOTH arrays have unprocessed elements. Each iteration adds exactly one element to `c`. |
| `if (a[i] < b[j])` | Compare current frontrunners. The smaller one goes into `c` next (and its pointer advances). |
| `while (i < n)` | If `b` ran out first, copy remaining `a` elements directly — they're already in order and all larger than everything in `c` so far. |
| `while (j < m)` | Symmetric: if `a` ran out, copy remaining `b` elements. |

**Concrete trace — merging `{1, 4, 7}` and `{2, 5, 6}`:**
```
i=0, j=0, k=0:  a[0]=1 < b[0]=2  →  c[0]=1,  i=1
i=1, j=0, k=1:  a[1]=4 > b[0]=2  →  c[1]=2,  j=1
i=1, j=1, k=2:  a[1]=4 < b[1]=5  →  c[2]=4,  i=2
i=2, j=1, k=3:  a[2]=7 > b[1]=5  →  c[3]=5,  j=2
i=2, j=2, k=4:  a[2]=7 > b[2]=6  →  c[4]=6,  j=3
j=3 = m → exit main while loop
i=2 < n=3: copy remaining a: c[5]=7
Result: {1, 2, 4, 5, 6, 7}  ✅
```

**Why exactly two cleanup `while` loops?** After the main loop, at most ONE of `a` or `b` will have leftover elements (not both — one ran out to exit the main loop). The first cleanup loop handles leftover `a`, the second handles leftover `b`. Exactly one of them will execute; the other does nothing (its condition is already false). Forgetting either means silently dropping those elements.

**Common wrong answers to watch for:** Forgetting either cleanup `while` → missing trailing elements. Declaring `int c[n+m]` before reading n and m → variable-length array declared before its size is known (undefined behavior). Off-by-one: `while (i <= n)` → reads `a[n]` which is out of bounds.

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
