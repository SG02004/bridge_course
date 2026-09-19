# NPTEL — Introduction to Programming in C (IIT Kanpur)
# Week 7 & 8 — Exam Notes

---

## 📌 Topic 1: Structures — Basics (`struct`, `.` operator, nested, init, assign) 📅 Week 7

### 1. Concept Summary
Real-world things are rarely a single number. A point on a plane has an `x` and a `y`, a student has a name, a roll number and marks. Before structs, you would keep these in separate variables or squeeze them into an array, but nothing in the language tied those pieces together, and an array can only hold one type anyway. A `struct` fixes this by letting you bundle variables of *different* types under one name, so the compiler treats "a point" or "a rectangle" as a single thing. Structs behave like first-class types: you can declare them, initialize them, assign one to another, pass them to functions, return them from functions, nest one inside another, and build arrays of them. Assignment (`s = r;`) copies every field's value one by one, which is why the two variables are independent afterward. The syntax quirks (the mandatory `;`, the `struct` keyword, initializer order) all follow from the fact that a struct definition is a *type declaration*, not a function body or a variable.

### 2. Key Syntax / Rules Box
```c
struct point {
    int x;
    int y;
};              // <-- semicolon after closing brace is MANDATORY

struct point pt;        // declaring a variable needs the 'struct' keyword
pt.x = 1;                // dot operator accesses a field
pt.y = 0;

struct point p = {0, 0}; // init: order must match field declaration order

struct rect {
    struct point leftbot;   // nested structure
    struct point righttop;
};
struct rect r = {{0,0}, {1,1}};   // nested braces mirror nesting
r.leftbot.x = 5;                   // chained dot operator

struct rect s;
s = r;   // structure assignment = member-wise (deep) copy, NOT a reference
```
- Missing the trailing `;` after `struct point {...}` is a compile error — a very common MCQ trap.
- `struct point;` alone does NOT create a variable — it's just the type; you need `struct point pt;`.
- You cannot compare two structs with `==` (not covered here explicitly, but commonly tested — C has no built-in struct comparison).
- Initializer list order follows **declaration order of fields**, not names.
- Assignment (`s = r;`) copies **all fields including nested ones** — it is a full/deep copy of values (not pointers), so modifying `s` afterward does NOT affect `r`.
- Arrays of structures: `struct point pts[6];` then `pts[i].x = i;` — index first, then dot.

### 3. Detailed Code Example
```c
#include <stdio.h>
#include <math.h>

struct point {
    int x;
    int y;
};

struct rect {
    struct point leftbot;
    struct point righttop;
};

// Passing struct BY VALUE (a copy is made — fine here since point is tiny)
double norm2(struct point p) {
    return sqrt(p.x * p.x + p.y * p.y);   // p is a local copy
}

// Returning a struct BY VALUE (safe: struct is copied out, not a dangling pointer)
struct point make_point(int x, int y) {
    struct point temp;
    temp.x = x;
    temp.y = y;
    return temp;                          // whole struct copied to caller
}

int main(void) {
    struct point pt = {3, 4};
    printf("%.1f\n", norm2(pt));          // 5.0

    struct rect r = {{0, 0}, {1, 1}};
    struct rect s;
    s = r;                                // member-wise copy
    s.leftbot.x = 99;                     // only changes s, not r
    printf("%d %d\n", r.leftbot.x, s.leftbot.x); // 0 99

    struct point pts[3];
    for (int i = 0; i < 3; i++) {
        pts[i] = make_point(i, i * 2);    // array of structs, each from a function
    }
    printf("%d %d\n", pts[2].x, pts[2].y); // 2 4
    return 0;
}
```

**What would NPTEL ask about this?**
- ❓ After `s = r;` and then `s.leftbot.x = 99;`, what is `r.leftbot.x`? → ✅ `0` → 💡 Struct assignment is a deep/member-wise copy, not aliasing — `s` and `r` are independent after `=`.
- ❓ What if you forget the `;` after `struct rect { ... }`? → ✅ Compile-time error → 💡 The closing brace of a struct definition must be followed by a semicolon, unlike a function body.
- ❓ `struct point p = {1, 2, 3};` — what happens? → ✅ Compile error / warning (excess initializer) → 💡 The struct only has 2 fields (`x`, `y`); you cannot provide more initializer values than fields.

### 5. Quick Recall
- `struct` = user-defined type grouping different-typed fields.
- `.` = access field on a struct *value* (not pointer).
- Struct definition **must** end with `;`.
- Structs are first-class: declare / init / assign / pass / return, just like `int`.
- `struct A x = y;` copies **every field**, including nested ones — deep, not aliased.

---

## 📌 Topic 2: Pointers to Structures & the Arrow Operator (`->`) 📅 Week 7

### 1. Concept Summary
When you pass a struct to a function by value, C copies every single field onto the function's stack. That is harmless for a tiny `struct point`, but for a large or deeply nested struct it wastes time and memory on every call. The fix is to pass a *pointer* to the struct instead, since an address has a small fixed size no matter how big the struct is. The catch is syntax: to reach a field through a pointer you must dereference first and then use `.`, but the dot operator binds tighter than `*`, so `*p.x` is parsed as `*(p.x)` and fails. You therefore need parentheses, `(*p).x`, and because that is clumsy C provides the arrow `p->x` as exactly equivalent shorthand. One more rule follows from how memory works: if a function returns a pointer to a struct, that struct must live on the heap, because a local struct is destroyed when the function returns.

### 2. Key Syntax / Rules Box
```c
struct Rectangle *pr;          // pointer to a struct
struct Rectangle r = {{0,0},{1,1}};
pr = &r;                       // pr now points to r

int x1 = (*pr).left_bot.x;     // correct: parentheses force deref first
int x2 = pr->left_bot.x;       // same thing, cleaner — PREFERRED

// WRONG:
// int x3 = *pr.left_bot.x;    // parses as *(pr.left_bot.x) -> ERROR
//                              // because '.' binds tighter than '*'
```
- `.` (dot) has **higher precedence** than `*` (dereference) — this is the #1 MCQ trap in this topic.
- `->` and `.` have the **same precedence** and are **left-associative**.
- `pointer->member` is *exactly* equivalent to `(*pointer).member` — memorize this equivalence, it's asked directly.
- If a function must **return a pointer** to a struct, that struct MUST be heap-allocated (`malloc`/`calloc`). Returning the address of a **local/stack** struct → dangling pointer → undefined behavior.

### 3. Detailed Code Example
```c
#include <stdio.h>
#include <stdlib.h>

struct Point { int x; int y; };
struct Rectangle { struct Point left_bot; struct Point right_top; };

// Efficient: only an address (4/8 bytes) is copied, regardless of struct size
int calculateAreaEfficient(struct Rectangle *pr) {
    return (pr->right_top.x - pr->left_bot.x) *      // arrow op: clean member access
           (pr->right_top.y - pr->left_bot.y);
}

// Returns a pointer safely because the struct lives on the HEAP
struct Rectangle* makeRectOnHeap(int x1, int y1, int x2, int y2) {
    struct Rectangle *pr = malloc(sizeof(struct Rectangle)); // heap, survives function return
    pr->left_bot.x = x1;  pr->left_bot.y = y1;
    pr->right_top.x = x2; pr->right_top.y = y2;
    return pr;                                       // safe: not a stack address
}

int main(void) {
    struct Rectangle r = {{0, 0}, {4, 3}};
    printf("Area = %d\n", calculateAreaEfficient(&r));   // 12

    struct Rectangle *heapRect = makeRectOnHeap(0, 0, 2, 2);
    printf("Heap area = %d\n", calculateAreaEfficient(heapRect)); // 4
    free(heapRect);                                    // must free heap memory
    return 0;
}
```

**What would NPTEL ask about this?**
- ❓ Is `*pr.left_bot.x` the same as `(*pr).left_bot.x`? → ✅ No → 💡 `.` has higher precedence than `*`, so `*pr.left_bot.x` illegally tries `pr.left_bot` first (pr is a pointer, `.` doesn't apply to pointers) → compile error.
- ❓ What's wrong with this function?
```c
struct Point* getOrigin(void) {
    struct Point p = {0, 0};   // local/stack variable
    return &p;                  // BUG
}
```
  → ✅ Returns a dangling pointer (undefined behavior) → 💡 `p` is destroyed when the function returns; its stack memory can be reused. Fix: `malloc` a `struct Point` instead.
- ❓ `pr->x` vs `(*pr).x` — which is more efficient at runtime? → ✅ Identical — same compiled code → 💡 `->` is pure syntactic sugar, not a performance feature.

### 5. Quick Recall
- Pass-by-value struct = full copy (slow for big structs); pass-by-pointer = just an address (fast).
- `.` binds tighter than `*` → always need `(*p).field` or `p->field`.
- `p->field` ≡ `(*p).field`, same precedence/associativity as `.`.
- Returning a pointer to a struct? → struct **must** be on the heap.

---

## 📌 Topic 3: Singly Linked Lists 📅 Week 7

### 1. Concept Summary
Arrays are fast to index but rigid: their size is fixed up front, and inserting or deleting in the middle means shifting every element after that point. A linked list drops the idea of contiguous storage. Each element is a separate node holding its data plus a pointer to the next node, and the whole list is reached through a `head` pointer, with `NULL` marking the end. Because a node contains a pointer to its own type, the structure is called self-referential, and the pointer is mandatory: a node that literally contained another node would have infinite size. Insertion and deletion become cheap pointer updates (O(1) once you are at the right spot), but you pay for it by losing random access, so searching is always O(n) and binary search is impossible even on sorted data. Order of operations matters when re-linking: you must connect the new node to the rest of the list *before* overwriting the old link, or the rest of the list is lost.

### 2. Key Syntax / Rules Box
```c
struct node {
    int data;
    struct node *next;   // MUST be a pointer, not "struct node next;"
};                        // (else infinite recursive size -> compile error)

typedef struct node *ListNode;  // optional convenience alias

struct node* make_node(int val) {
    struct node* temp = (struct node*)calloc(1, sizeof(struct node));
    if (temp == NULL) return NULL;      // always check malloc/calloc!
    temp->data = val;
    temp->next = NULL;                  // new node always ends the chain (for now)
    return temp;
}
```
- `struct node *next;` — pointer is mandatory; `struct node next;` inside itself is illegal (infinite size).
- Empty list ⇔ `head == NULL`.
- End of list ⇔ `node->next == NULL`.
- Search / traversal is always **O(n)** — even if data happens to be sorted, you cannot binary-search a linked list (no random access).
- Deleting a node needs a pointer to its **previous** node too, since you can't go backward in a singly linked list.

### 3. Detailed Code Example
```c
#include <stdio.h>
#include <stdlib.h>

struct node { int data; struct node *next; };

struct node* make_node(int val) {
    struct node* temp = calloc(1, sizeof(struct node));
    temp->data = val;
    temp->next = NULL;
    return temp;
}

// Insert at front: O(1) — no traversal needed
struct node* insert_front(int val, struct node* head) {
    struct node* new_node = make_node(val);
    new_node->next = head;   // MUST happen before head is reassigned
    head = new_node;
    return head;
}

// Insert after a given node p_current: order of steps matters!
struct node* insert_after(struct node* p_current, int val) {
    struct node* p_new = make_node(val);
    p_new->next = p_current->next;  // (1) link new node to the REST of the list first
    p_current->next = p_new;        // (2) then link predecessor to new node
    return p_new;
}

struct node* search(struct node* head, int key) {
    struct node* curr = head;
    while (curr != NULL && curr->data != key) {
        curr = curr->next;
    }
    return curr;                     // NULL if not found
}

int main(void) {
    struct node* head = NULL;
    head = insert_front(3, head);    // list: 3
    head = insert_front(2, head);    // list: 2 -> 3
    head = insert_front(1, head);    // list: 1 -> 2 -> 3
    insert_after(head, 99);          // list: 1 -> 99 -> 2 -> 3

    struct node* found = search(head, 2);
    printf("%s\n", found ? "Found" : "Not found");  // Found

    for (struct node* c = head; c != NULL; c = c->next)
        printf("%d ", c->data);      // 1 99 2 3
    return 0;
}
```

**What would NPTEL ask about this?**
- ❓ In `insert_after`, what breaks if you swap the two lines to `p_current->next = p_new;` FIRST, then `p_new->next = p_current->next;`? → ✅ You lose the rest of the list — `p_new->next` becomes `p_new` itself (self-loop) or garbage → 💡 Once `p_current->next` is overwritten first, its original value (the rest of the list) is gone forever.
- ❓ What does `struct node { int data; struct node next; };` (no `*`) cause? → ✅ Compile error → 💡 Infinite recursive size — the compiler can't determine `sizeof(struct node)` since it contains itself.
- ❓ Can you binary-search a sorted singly linked list in O(log n)? → ✅ No, still O(n) → 💡 Binary search needs O(1) random access to the "middle" element, which linked lists don't provide — you must traverse node by node to get anywhere.

### 5. Quick Recall
- `next` field **must** be a pointer (self-referential structure).
- `head == NULL` → empty list; `node->next == NULL` → last node.
- `insert_front` = O(1); `search`/`insert_after` (finding the point) = O(n) traversal.
- In `insert_after`: link new→successor **before** predecessor→new.
- Deletion needs the *previous* node's pointer — can't go backward otherwise.
- Linked lists: fast insert/delete (O(1) at known point), slow search (O(n)), no binary search.

---

## 📌 Topic 4: Doubly Linked Lists 📅 Week 7

### 1. Concept Summary
A singly linked list only moves forward, which creates an annoying problem: to insert before a node or delete a node, you need its predecessor, and the only way to find it is to walk the list from the head, an O(n) trip. A doubly linked list solves this by giving every node a `previous` pointer as well as a `next` pointer, and by keeping both a `Head` and a `Tail` pointer for the list as a whole. Now, given a pointer to any node, you can reach both neighbours instantly, so `insert_before` and `delete_node` drop to O(1). The price is extra memory per node and more bookkeeping, since every insertion or deletion must fix up pointers in both directions and handle three different situations (head, tail, middle) separately. Note what does *not* improve: finding an unknown value still means checking nodes one at a time, so search stays O(n).

### 2. Key Syntax / Rules Box
```c
struct dllnode {
    int data;
    struct dllnode *next;      // NULL for the last node
    struct dllnode *previous;  // NULL for the first node
};
// List usually tracked via a wrapper holding Head and Tail pointers
```
- Both `next` (of tail) and `previous` (of head) are `NULL`.
- `insert_before(L, pcurr, pnew)` — O(1) once `pcurr` is known (vs O(n) in singly linked list, since you'd need to find the predecessor by traversal there).
- `delete_node` has **3 cases**: deleting head, deleting tail, deleting a middle node — each updates different pointers.
- `extract_node` = same pointer surgery as `delete_node` but does **not** `free()` the node — it returns it instead.
- Search is STILL O(n) — bidirectional links don't help search speed.

### 3. Detailed Code Example
```c
#include <stdio.h>
#include <stdlib.h>

struct dllnode { int data; struct dllnode *next; struct dllnode *previous; };

// Delete node p, given the list's head/tail pointers (passed by address to update them)
void delete_node(struct dllnode **head, struct dllnode **tail, struct dllnode *p) {
    if (p == *head) {                                 // Case 1: deleting head
        *head = p->next;
        if (*head != NULL) (*head)->previous = NULL;
    } else if (p == *tail) {                          // Case 2: deleting tail
        *tail = p->previous;
        if (*tail != NULL) (*tail)->next = NULL;
    } else {                                           // Case 3: middle node
        p->previous->next = p->next;                   // bypass p forward
        p->next->previous = p->previous;                // bypass p backward
    }
    free(p);
}

int main(void) {
    // Build list: 1 <-> 2 <-> 3
    struct dllnode *n1 = malloc(sizeof(struct dllnode));
    struct dllnode *n2 = malloc(sizeof(struct dllnode));
    struct dllnode *n3 = malloc(sizeof(struct dllnode));
    n1->data = 1; n2->data = 2; n3->data = 3;
    n1->previous = NULL; n1->next = n2;
    n2->previous = n1;   n2->next = n3;
    n3->previous = n2;   n3->next = NULL;

    struct dllnode *head = n1, *tail = n3;
    delete_node(&head, &tail, n2);   // delete middle node

    printf("%d -> %d\n", head->data, head->next->data);  // 1 -> 3
    printf("Tail prev: %d\n", tail->previous->data);      // 1
    return 0;
}
```

**What would NPTEL ask about this?**
- ❓ In a doubly linked list, is `insert_before` O(1) or O(n)? → ✅ O(1), once you have a pointer to the target node → 💡 `pcurr->previous` gives instant access to the predecessor — no traversal needed, unlike singly linked lists.
- ❓ After deleting the tail node, what must be updated? → ✅ `tail = p->previous;` and then `tail->next = NULL;` → 💡 Skipping the second step leaves the new tail's `next` pointing to freed memory (dangling pointer).
- ❓ Does a doubly linked list improve search time complexity? → ✅ No, still O(n) → 💡 Bidirectional traversal helps *movement*, not *locating* an unknown element — you still must check nodes one by one.

### 5. Quick Recall
- DLL node = `data + next + previous`; SLL node = `data + next` only.
- `insert_before` / `delete_node` (node known) = O(1) in DLL vs O(n) in SLL.
- 3 delete cases: head / tail / middle — each touches different pointers.
- `extract_node` = pointer surgery without `free()`.
- Search is O(n) regardless — bidirectionality doesn't speed up search.

---

## 📌 Topic 5: Organizing Code into Multiple Files 📅 Week 8

### 1. Concept Summary
Once a program grows past a few hundred lines, keeping everything in one file becomes painful: every small edit forces a full recompile, several people cannot easily work in parallel, and there is no clean boundary between "what this code offers" and "how it does it". C's answer is to split code into header files (`.h`) and source files (`.c`). The header is the *interface*: it holds only declarations such as function prototypes, structs and typedefs. The `.c` file is the *implementation*: the actual function bodies. Each `.c` file is compiled on its own into an object file (`gcc -c`), and the linker then stitches the object files into one executable. This is why changing only `prog.c` means recompiling just `prog.c` and re-linking, while `list.o` is reused. Other files use a module by including its `.h` (never its `.c`), which also hides implementation details, and a module that allocates memory should ship a matching free function so callers don't leak.

### 2. Key Syntax / Rules Box
```bash
gcc -c list.c        # compiles list.c -> list.o  (compile only, no link)
gcc -c prog.c        # compiles prog.c -> prog.o
gcc prog.o list.o -o prog   # LINKS object files into executable "prog"
                             # (if -o omitted, default name is a.out)
```
```c
// prog.c includes the HEADER, never the .c file directly
#include "list.h"    // double quotes: search current dir FIRST, then system paths
#include <stdio.h>   // angle brackets: search ONLY system/standard directories
```
- `prog.c` should `#include "list.h"` — **never** `#include "list.c"`.
- `.h` files should contain **declarations only** (prototypes, `struct`/`typedef`), not variable initializations or executable code (that's bad practice and can duplicate code across files).
- If only `prog.c` changes, only `prog.o` needs recompiling — `list.o` is reused. This is the key "why multi-file" exam point.
- A library allocating memory (e.g. `makeNode()`) should also provide a matching free function (`freeList()`), for information hiding + safe memory management.

### 3. Detailed Code Example
```c
/* ---------- list.h (HEADER: declarations only) ---------- */
#ifndef LIST_H
#define LIST_H

struct node { int data; struct node *next; };
struct node* make_node(int val);   // prototype only, no body
void print_list(struct node *head);

#endif // LIST_H

/* ---------- list.c (SOURCE: implementation) ---------- */
#include <stdio.h>
#include <stdlib.h>
#include "list.h"                   // include own header to check prototypes match

struct node* make_node(int val) {
    struct node *n = malloc(sizeof(struct node));
    n->data = val;
    n->next = NULL;
    return n;
}

void print_list(struct node *head) {
    for (struct node *c = head; c != NULL; c = c->next)
        printf("%d ", c->data);
    printf("\n");
}

/* ---------- prog.c (USES the list module) ---------- */
#include "list.h"    // NOT "list.c" -- only need the interface

int main(void) {
    struct node *head = make_node(10);
    head->next = make_node(20);
    print_list(head);               // 10 20
    return 0;
}
```
Build commands:
```bash
gcc -c list.c       # -> list.o
gcc -c prog.c       # -> prog.o
gcc prog.o list.o -o prog
./prog
```

**What would NPTEL ask about this?**
- ❓ If you edit only `prog.c`, which files must be recompiled? → ✅ Only `prog.c` → `prog.o`; `list.o` is reused, then re-link → 💡 Separate compilation means unchanged `.c` files don't need recompiling — this is the entire point of multi-file builds.
- ❓ What happens if `prog.c` does `#include "list.c"` instead of `"list.h"`? → ✅ It compiles (copy-paste), but you lose the benefits of separate compilation and may get "multiple definition" linker errors if `list.c` is also compiled and linked separately → 💡 `.c` files contain definitions; including one directly duplicates code across translation units.
- ❓ `#include <myheader.h>` vs `#include "myheader.h"` for your OWN project header — which is correct convention, and what's the practical risk of using the wrong one? → ✅ Use double quotes `"myheader.h"` → 💡 Angle brackets only search standard system directories, so the compiler may fail to find your custom header (or, worse, silently pick up an unrelated system file of the same name).

### 5. Quick Recall
- `.h` = declarations (interface); `.c` = definitions (implementation).
- `gcc -c file.c` → `file.o` (compile only); `gcc a.o b.o -o out` → link.
- `""` searches current dir first, then system; `<>` searches system dir only.
- Only changed `.c` files need recompiling — that's the whole efficiency win.
- Never `#include` a `.c` file — always its `.h`.

---

## 📌 Topic 6: The C Preprocessor (`#include`, `#define`, `#ifndef` / Include Guards) 📅 Week 8

### 1. Concept Summary
Before the compiler ever looks at your code, a separate tool called the preprocessor runs over it. It knows nothing about C types or syntax; it is a pure text editor that acts on lines beginning with `#`. `#include` pastes the contents of another file at that exact spot, and `#define` sets up a textual replacement (so `BUF_SZ` becomes `1024` everywhere after the definition). Because it works strictly top to bottom, a `#define` only affects the lines that come *after* it. This blind pasting creates a real problem with headers: if the same header reaches a file twice (say directly and through another header), its contents are pasted twice and you get errors like "redefinition of struct node". Include guards (`#ifndef` / `#define` / `#endif`) solve this: the first time the header is seen the guard name is undefined, so the content is kept and the name gets defined; every later time the name is already defined, so the content is skipped. The full pipeline is preprocessor → compiler → linker, and `gcc` runs all three when you type one command.

### 2. Key Syntax / Rules Box
```c
#define BUF_SZ 1024              // object-like macro; convention: UPPER_CASE
char *buf = malloc(BUF_SZ);      // preprocessor replaces BUF_SZ -> 1024 (pure text sub)

foo = X;
#define X 4
bar = X;
// After preprocessing: foo = X;  (X undefined here -> left as-is / error)
//                       bar = 4; (X is now defined)

// Include guard -- standard boilerplate for every header file
#ifndef LIST_H
#define LIST_H
// ... all declarations ...
#endif
```
- `#define` is a **sequential**, textual substitution — only affects code written AFTER the `#define` line.
- Include guards use exactly 3 directives: `#ifndef NAME`, `#define NAME`, `#endif`.
- The FIRST time a header is included, its guard macro is undefined → content is processed AND the macro gets defined. On every SUBSEQUENT include (even from a different file, same compilation unit), the guard macro is already defined → content is skipped.
- Compilation pipeline order: **Preprocessor → Compiler (→ assembly → object file) → Linker**.
- `#include` = literal copy-paste of file contents at that exact line — nothing more, nothing "smart" about types.

### 3. Detailed Code Example
```c
/* ---------- list.h ---------- */
#ifndef LIST_H
#define LIST_H

#define MAX_NODES 100          // object-like macro, usable by anyone including this header

struct node { int data; struct node *next; };

#endif // LIST_H

/* ---------- p1.h ---------- */
#ifndef P1_H
#define P1_H
#include "list.h"              // list.h processed here (1st time): LIST_H gets defined
#endif

/* ---------- p2.c ---------- */
#include "p1.h"                 // pulls in list.h via p1.h
#include "list.h"                // 2nd attempt to include list.h directly:
                                  // LIST_H is ALREADY defined -> #ifndef is false -> SKIPPED
                                  // avoids "redefinition of struct node" error

int main(void) {
    struct node arr[MAX_NODES]; // both struct node and MAX_NODES available exactly once
    (void)arr;
    return 0;
}
```

**What would NPTEL ask about this?**
- ❓ In `p2.c` above, without the include guard in `list.h`, what error occurs? → ✅ "redefinition of `struct node`" compile error → 💡 `list.h`'s content gets pasted twice (once via `p1.h`, once directly), so `struct node` is textually defined twice in the same translation unit.
- ❓ Given `foo = X; #define X 4; bar = X;` — what is the value used for `foo`? → ✅ `X` is undefined at that point → compile error (or, if `X` was previously a variable, it stays as that variable) → 💡 `#define` only affects code appearing *after* it — preprocessing is strictly sequential/top-to-bottom.
- ❓ Which comes first in the pipeline: preprocessing or compiling to object code? → ✅ Preprocessing → 💡 Order is Preprocessor → Compiler → Linker; `gcc` runs all three silently when you type one command.

### 5. Quick Recall
- Order: **Preprocessor → Compiler → Linker**.
- `#include "x.h"` = literal text paste at that line.
- `#define NAME value` = simple text substitution, UPPER_CASE convention, sequential effect only.
- Include guard = `#ifndef GUARD` / `#define GUARD` / ... / `#endif` — prevents double-definition errors.
- A `#define` placed after some code does **not** retroactively affect that earlier code.

---

## 📌 Topic 7: Pre & Post Increment Operators, Side Effects, Sequence Points 📅 Week 8

### 1. Concept Summary
`++i` and `i++` both add one to `i`, but they differ in the *value the expression produces*. With `++i` the increment happens first and the expression gives you the new value; with `i++` the expression gives you the original value, and the increment is applied as a side effect sometime before the next sequence point (roughly, the end of the full expression). An expression has a side effect when it changes a variable in addition to computing a value, and that is exactly where trouble starts. C only guarantees that side effects are complete at sequence points such as `;`, `&&`, `||`, `?:`, `,` and function-call boundaries, and it does not fix the order in which sub-expressions are evaluated. So if you modify the same variable more than once between two sequence points (`i++ + i++`, or `j = j++`), the standard doesn't say what result you get. NPTEL calls this *unspecified behavior* (the "at most once" rule). The practical habit is simple: one side effect per variable per statement, and split anything trickier into separate statements.

### 2. Key Syntax / Rules Box
```c
int i = 1, j;
j = ++i;   // i becomes 2 FIRST, then j = 2.   (i=2, j=2)

int i = 1, j;
j = i++;   // j gets ORIGINAL i (1) first, THEN i becomes 2.   (i=2, j=1)

// Sequence points: end of full expression (;), function-call boundary
// (all args evaluated before call), &&, ||, ?:, comma operator

int i = 1;
int j = i++ + i++;   // UNSPECIFIED BEHAVIOR: i modified twice before next sequence point

int j = 1;
j = j++;             // UNSPECIFIED BEHAVIOR: j modified by both j++ AND the assignment
```
- Pre-increment equivalent: `i = i + 1; j = i;`
- Post-increment equivalent: `temp = i; i = i + 1; j = temp;`
- **"At most once" rule**: a variable can be modified **at most once** by an expression between two sequence points. Break this → **unspecified behavior** (not "undefined behavior" — different term, but still avoid it; NPTEL specifically uses "unspecified").
- Order of evaluation of sub-expressions (e.g., `f() + g()` — who runs first?) is also unspecified by the C standard.
- Fix for unsafe expressions: split into multiple simple statements.

### 3. Detailed Code Example
```c
#include <stdio.h>

int main(void) {
    int i = 1, j;

    j = ++i;                 // i=2, j=2 (pre-increment: update then use)
    printf("%d %d\n", i, j); // 2 2

    i = 1;
    j = i++;                 // i=2, j=1 (post-increment: use then update)
    printf("%d %d\n", i, j); // 2 1

    // Combined expression (well-defined: each variable touched only once)
    i = 3; j = 1;
    int k = ++i + j++;       // ++i -> i=4, uses 4 ; j++ -> uses 1, j becomes 2 later
    printf("i=%d j=%d k=%d\n", i, j, k);  // i=4 j=2 k=5

    // UNSPECIFIED BEHAVIOR EXAMPLES -- avoid writing these, but recognize them on exam!
    // int x = 1;
    // int y = x++ + x++;     // x modified twice before next ';' -> unspecified
    // int z = 1;
    // z = z++;               // z modified by both z++ and '=' -> unspecified

    // SAFE rewrite of the risky pattern above:
    int x = 1;
    int y = x++;              // step 1: y=1, x=2
    y = y + x++;              // step 2: y=1+2=3, x=3  (each statement modifies x at most once)
    printf("x=%d y=%d\n", x, y); // x=3 y=3

    return 0;
}
```

**What would NPTEL ask about this?**
- ❓ `int i=5; int j = i++ + ++i;` — what is the value of `j`? → ✅ Unspecified/compiler-dependent (a valid MCQ answer choice is often "cannot be determined" or "undefined/unspecified behavior") → 💡 `i` is modified by both `i++` and `++i` before the next sequence point (the semicolon) — this violates the "at most once" rule.
- ❓ `int i=1; int j=1; int k = i++ + (i+1);` — is this well-defined? → ✅ No, unspecified → 💡 `i` is both modified (`i++`) and read again in `(i+1)` within the same expression before a sequence point, and the order of evaluation between the two sub-expressions is unspecified.
- ❓ Simple check: `int i=1; int j = i++;` What are the final values of `i` and `j`? → ✅ `i=2, j=1` → 💡 Post-increment returns the ORIGINAL value; the increment is applied as a side effect that must complete by the next sequence point, but the value used in the expression is the pre-increment value.

### 5. Quick Recall
- `++i`: increment FIRST, then use new value.
- `i++`: use OLD value FIRST, increment happens by next sequence point.
- Sequence points: `;` (end of full expression), function-call arg evaluation, `&&`, `||`, `?:`, `,`.
- "At most once" rule: modifying the same variable more than once between sequence points = **unspecified behavior**.
- Order of evaluation of sub-expressions (e.g. left/right of `+`) is also unspecified — don't rely on it.
- When in doubt: break complex expressions into separate simple statements.

---

## 🧪 Weekly Assignment Analysis

⚠️ **No assignment questions were found in the uploaded transcript file** (`week7and8merged.md`) — it only contained the 9 lecture transcripts (w7p1–w7p5, w8p1–w8p4), no MCQ/MSQ assignment content.

Please paste the actual Week 7 and Week 8 assignment questions (with the options shown, if MCQ/MSQ) in your next message, and I'll add the full **question → correct answer → explanation (including why wrong options are wrong)** section here, matching the format above.
