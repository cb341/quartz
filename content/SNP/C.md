## Preprocessor & Headers

### include guards

Stop double declaration errors caused by multiple inclusion.

```c
#ifndef MY_HEADER_H
#define MY_HEADER_H
struct Node { int val; };
#endif
```

### conditional compilation

Include or skip code blocks for debugging or production modes.

```c
#ifdef DEBUG_MODE
    printf("Debug active\n");
#endif
```

## Basic Data Types & Coercion

### value ranges

Bit widths depend on hardware. Limits are checked via `limits.h`.

### integer promotion

Compiler converts shorter integer types to wider types automatically.

## Structs & Unions

### recursive structures

A struct cannot contain itself, but can contain a pointer to its own type for linked lists or trees.

```c
struct Node {
    int data;
    struct Node* next; /* recursive pointer */
;
```

### structure alignment

Compiler inserts padding gaps to satisfy memory alignment requirements, making `sizeof(struct)` larger than its fields.

https://padding-split.vercel.app/

## Arrays & Strings

### array decays to pointer

The array name is the address of the first element.

### jagged array via compound literals

A two-dimensional array where rows have different column counts.

```c
int (*(arr[])) = { (int[]) {0, 1, 2, 3}, (int[]) {4, 5} };
```

### string NUL termination

Strings must end with a `\0` (NUL) character.

## Pointers & Arithmetic

### differences: int*, &, and []

* **`int *ptr`**: Declares pointer.

* **`&var`**: Address-of operator.

* **`[]`**: Array declaration or offset access.



### pointer modifier variations

* `const int *p`: Data is constant.

* `int * const p`: Address is constant.



## Concurrency

### threads & mutex

Mutex locks protect "critical sections" from simultaneous access. Recursive mutexes allow nested locks by the same thread.

```c
pthread_mutex_lock(&mutex);
counter++; /* critical section */
pthread_mutex_unlock(&mutex);
```

## System I/O & Signals

### syscalls vs stdio

Syscalls (`open`, `read`) are unbuffered kernel interfaces. `stdio` (`fopen`, `fprintf`) provides user-space buffering.

### signal handling

`sigaction` registers routines to handle asynchronous OS interrupts like `SIGINT` (Ctrl+C).

