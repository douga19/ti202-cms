---
theme: default
background: #e9e9e9
class: cover
highlighter: shiki
lineNumbers: false
info: |
  ## TI202 - Data Structures and Programming 1
  Lecture 3 - Pointers and Dynamic Memory Allocation
drawings:
  persist: false
transition: slide-left
title: CM3 - Pointers and Dynamic Memory Allocation
mdc: true
colorSchema: light
canvasWidth: 1000
---

<style>
:root {
  --slidev-theme-primary: #377fbc;
  --slidev-theme-secondary: #ff43b8;
}

h1, h2, h3, h4, h5, h6 {
  color: #163767 !important;
  font-weight: 700;
}

strong {
  color: #ff43b8;
  font-weight: 600;
}

em {
  color: #377fbc;
  font-style: italic;
}

table {
  border-collapse: collapse;
  width: 100%;
  margin: 1rem 0;
  background: #f8f9fa;
  border-radius: 8px;
  overflow: hidden;
}

table th {
  background: #377fbc;
  color: #e9e9e9;
  padding: 12px;
  text-align: left;
  border-bottom: 2px solid #ff43b8;
  font-weight: 700;
}

table td {
  padding: 10px 12px;
  border-bottom: 1px solid #e0e7ff;
  color: #051832;
}

table tr:hover {
  background: rgba(55, 127, 188, 0.08);
}

.tag {
  display: inline-block;
  background: rgba(255, 67, 184, 0.15);
  color: #ff43b8;
  padding: 4px 12px;
  border-radius: 20px;
  font-size: 0.85em;
  border: 1px solid #ff43b8;
  margin: 2px 4px;
  font-weight: 600;
}

a {
  color: #377fbc;
  text-decoration: underline;
}

a:hover {
  color: #ff43b8;
}

blockquote {
  border-left: 10px solid #ff43b8;
  background: #f0f4f8;
  margin-top: 1em;
  padding: 1em;
  border-radius: 4px;
  color: #163767;
}

.two-cols-header {
    column-gap: 20px; /* Adjust the gap size as needed */
}
</style>


# Pointers and Dynamic Memory Allocation

TI202 - Data Structures and Programming 1

**Rado Rakotonarivo**  
*Based on Asma Gabis' Course*

---

# Course Outline

<v-clicks>

1. **Pointers**
   - Memory Representation
   - Pointer Declaration and Manipulation
   - Pointers to Pointers

2. **Pointers & Arrays**
   - Relationship between Arrays and Pointers
   - 2D Arrays and Pointers

3. **Dynamic Memory Allocation**
   - `malloc()`, `calloc()`, `free()`, `realloc()`
   - Dynamic Allocation of 2D Arrays

4. **Application**

</v-clicks>

---
layout: intro
---

# Pointers

---

## RAM Memory Representation

<v-clicks>

- When a program is executed, a portion of the computer's **RAM (Random Access Memory)** is allocated to store the data used by the program (variables, instructions, etc.).
- This memory is organized in **memory cells** (or bytes) identified by unique **memory addresses**.
- RAM resembles a **table divided into sequentially numbered cells**.

```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│  0  │  1  │  2  │  3  │  4  │  5  │ ... │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┘
```

### Characteristics

- Memory cell numbers **start at 0**
- Each cell size is **1 byte** (8 bits)
- Total size depends on the machine

</v-clicks>

---

## Variable Storage in Memory

<v-clicks>

When a variable is declared, a **memory location** is reserved to store its value.

### Example
```c
char c;
c = 'C';
```

<div grid="~ cols-2 gap-4">

<div>

**Memory Representation:**

```
┌─────────┬────────┬─────┐
| Address | Value  | Name |
|---------|--------|-----|
| ...     | ...    |     |
| @1599   |        |     |
| @1600   | 'C'    |  c  |
| @1601   |        |     |
| ...     | ...    |     |

```

> ⚠️ The memory address of a variable is the address of its **first byte**

</div>

<div>

### Key Points

- **Memory address** : @1600 (where `c` is stored)
- **Value** : `'C'` (stored in `c`)
- **Symbolic name** : `c` (to access the variable)
- Memory addresses are represented in **hexadecimal**

> ⚠️ For this course, addresses will be represented in **decimal prefixed by `@`**

</div>

</div>

</v-clicks>

---

## Variable Size

<v-clicks>

Variable values don't always occupy a single memory cell → This depends on their **types**.

### Typical Sizes (machine-dependent)
- `char` : **1 byte**
- `int` : **4 bytes**
- `double` : **8 bytes**

### The `sizeof` Operator

`sizeof` returns the number of bytes a type occupies:

```c
#include <stdio.h>

int main() {
    printf("The char type occupies %lu bytes in memory.\n", sizeof(char));
    printf("The int type occupies %lu bytes in memory.\n", sizeof(int));
    printf("The double type occupies %lu bytes in memory.\n", sizeof(double));
    return 0;
}
```

> `%lu` : format for displaying an unsigned long integer

</v-clicks>

---

## Variable Size : Effect of Memory Storage

<div grid="~ cols-3 gap-4">

<v-clicks>

<div>

```c
char c = 'C'; // 1 byte
```

| Address | Value |
|---------|--------|
| @1599    | ...    |
| **@1600** | **'C'** |
| @1601    | ...    |

</div>

<div>

```c
int x = 3; // 4 bytes
```

| Address | Value |
|---------|--------|
| @1599    | ...    |
| **@1600** |        |
| **@1601** | **3**  |
| **@1602** |        |
| **@1603** |        |
| @1604    | ...    |

</div>

<div>

```c
double pi = 3.14; // 8 bytes
```

| Address | Value |
|---------|--------|
| @1599    | ...    |
| **@1600** |        |
| **@1601** |        |
| **@1602** | **3.14** |
| **@1603** |        |
| **@1604** |        |
| **@1605** |        |
| **@1606** |        |
| **@1607** |        |
| @1608    | ...    |

</div>

</v-clicks>

</div>

---

## Retrieving a Variable's Address

<v-clicks>

The **`&`** operator (ampersand) allows you to get a variable's address.

### Display Formats
- `%u` : unsigned integer (address in decimal)
- `%p`: pointer (address in hexadecimal)

### Example

```c
int main() {
    int var = 5;
    printf("The value of variable var is: %d\n", var);
    printf("The address of variable var is: %u\n", &var);
    printf("The address of variable var in hexadecimal is: %p\n", &var);
    return 0;
}
```

### ⚠️ Important
- The address displayed for a variable whose type occupies more than 1 byte is the address of its **first byte**
- The notation `&var` has already been seen in the `scanf` function syntax

</v-clicks>

---

# How to Get a Variable's Address? (continued)

<v-clicks>

### Reminder with `scanf`

```c
int main() {
    int var;
    scanf("%d", &var);  // Store the keyboard input
                        // in variable var using its address
    
    printf("The value of variable var is: %d\n", var);
    printf("The address of variable var in hexadecimal is: %p\n", &var);
    return 0;
}
```

### Explanation
`&var` allows `scanf` to know the **memory address** where to store the input value.

</v-clicks>

---

# Accessing a Variable

<v-clicks>

There are two ways to access a variable in memory:

### 1. Direct Access
The method used so far: access to the variable's contents is done via its **symbolic name**.

```c
int a = 10;
printf("%d", a);  // Direct access via the name
```

### 2. Indirect Access
Access to a variable is done through an **intermediate variable** containing its address.


</v-clicks>

---

## Indirect Access : Memory Representation

<v-clicks>

Access to a variable `a` is done through an intermediate variable `p` by storing the address of `a` in variable `p`.

<div grid="~ cols-2 gap-4">

<div>

| Address | Value | Variable |
|---------|--------|----------|
| ...     | ...    |          |
| @1000    | **@5424** | **p** |
| @1008    |        |          |
| ...     | ...    |          |
| @5424    | **10** | **a** |
| @5428    |        |          |

</div>

<div>

### Key Points
- **Value of `a`** = 10
- **Address of `a`** = @5424
- **Value of `p`** = @5424 (address of `a`)
- **Address of `p`** = @1000
- `p` is a **special** variable that contains a **memory address** of another variable.

</div>

</div>

</v-clicks>

---

# What is a Pointer?

<v-clicks>

### Definition
A pointer is a **variable** that is intended to **store the address of another variable**.

### Why Use a Pointer?

A pointer is used to **access a variable when direct access via its symbolic name is not possible or not desirable**.


### Advantages of a Pointer

- ⚡ **Direct memory access** and manipulation of its addresses → one of the most powerful fundamental principles of C programming (and C++)
- 🚀 **Very fast operations** : direct memory access from source code

</v-clicks>

---

## Pointer Manipulation : Declaration

<v-clicks>

The **`*`** character (asterisk) marks the pointer type.

### Syntax

```c
Type* Pointer_name;
```

<div grid="~ cols-2 gap-4">

<div>

### Syntax Elements
- **Type** : type of the data pointed to
- **\*** : means it is a pointer type
- **Pointer_name** : symbolic name (often starts with `p` or ends with `ptr`)

</div>

<div>

### Examples
```c
int main() {
    int x;    // Variable A
    char b;   // Variable B
    int* px = NULL;  // Pointer to int
    char *b_ptr = NULL;   // Pointer to char
    return 0;
}
```
</div>

</div>

- **`NULL`** special value indicating that the pointer points to a null address (invalid address).
- It is used to initialize a pointer before assigning it a valid address.
- Since pointers are variables, all known rules apply (assignment, initialization, etc.).


</v-clicks>

---

# Reference / Dereference Operators

<v-clicks>

### The `&` Operator (Reference)
- Called the **reference operator**
- When applied to a variable → It gives its **address**

### The `*` Operator (Dereference)
- Called the **dereference operator**
- Applied to a pointer-type variable
- It gives the **value** of the variable pointed to by the pointer (indirect access to the variable)

> ⚠️ The `*` operator cancels the effect of the `&` operator

</v-clicks>

---

# Complete Example : Pointer Manipulation

```c
#include <stdio.h>

int main() {
    int x;                  // declaration of variable x
    int* px = NULL;       // declaration of a pointer to an int variable
    x = 5;                  // initialization of variable x
    
    // Pointer initialization : to point to variable x
    px = &x;              // assign the address of x to px
    
    // Display the value of x normally
    printf("Direct access : The value of x is: %d \n", x);
    
    // Display the address of x normally
    printf("Direct access : The address of x is: %p \n", &x);  // using &
    
    // Display the value of x via the pointer
    printf("Indirect access : The value of x is: %d \n", *px);  // using *
    
    // Display the address of x via the pointer ==> display the pointer's value
    printf("Direct access : The value of px is: %p \n", px);
    
    return 0;
}
```

---

# Beware of Confusion ⚠️

<v-clicks>

Consider the following two variables:
```c
int c, *pc;  // declaration of a variable and a pointer on the same line
```

### Common Mistakes

<div grid="~ cols-2 gap-4">

<div>

#### ❌ WRONG
```c
pc = c;
```

`pc` is a pointer while `c` is not.

```c
*pc = &c;
```

`*pc` is a value while `&c` is an address.

</div>

<div>

#### ✅ CORRECT
```c
pc = &c;
```

`pc` is an address and so is `&c`.

```c
*pc = c;
```

`*pc` is the value pointed by `pc` and `c` is a value of the same type.

</div>

</div>

</v-clicks>

---
layout: image-right
image: /assets/pointer.jpg
backgroundSize: contain
---

## Pointer to Pointer

<v-clicks>

What happens when a pointer points to another pointer instead of a normal variable? → **Double Pointer**

### Declaration of a Double Pointer
```c
Type** Pointer_name;
```

### Memory Representation
```c
int x = 10;
int* px = &x;        // simple pointer 
int** ppx = &px;     // pointer to pointer
```

is represented in memory as follows:

```
   px              x             ppx
┌───────┬───────┬──────┬───────┬─────┐
│  @80  │  ...  │  10  │  ...  │ @64 │
└───────┴───────┴──────┴───────┴─────┘
   @64            @80            @104
```

</v-clicks>

---

# Pointer to Pointer : Example

```c
int x = 10;
int* px = &x;        // simple pointer 
int** ppx = &px;     // pointer to pointer
```

<v-clicks>

### Access to Values
- `x` : direct value (10)
- `*px` : value via simple pointer (10)
- `**ppx` : value via double pointer (10)
- `px` : address of x
- `*ppx` : address of x (same as px)
- `ppx` : address of px

</v-clicks>

---
layout: intro
---

# Pointers & Arrays

---

# What is the Relationship between an Array and a Pointer?

<v-clicks>

### Key Points

- The name of an array **evaluates** to the **memory address** of its **first element**
- An array is therefore represented by a pointer to the type of its elements

### Accessing Array Elements

**Reminder:** An array is stored in memory in a **contiguous** area → cells are positioned one after another.

```c
int T[] = {12, 78, 2, 65, 90, 1, 11, 45, 81};
```

is represented in memory as follows:

```
  T[0]   T[1]   T[2]   T[3]   T[4]   T[5]   T[6]   T[7]   T[8]
┌──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┐
│  12  │  78  │  2   │  65  │  90  │  1   │  11  │  45  │  81  │
└──────┴──────┴──────┴──────┴──────┴──────┴──────┴──────┴──────┘
```
</v-clicks>

---

# Array Representation with Pointers

<v-clicks>

### With Addresses

```
  T[0]   T[1]   T[2]   T[3]   T[4]   T[5]   T[6]   T[7]   T[8]
┌──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┐
│  12  │  78  │  2   │  65  │  90  │  1   │  11  │  45  │  81  │
└──────┴──────┴──────┴──────┴──────┴──────┴──────┴──────┴──────┘
  @80    @84    @88    @92    @96    @100   @104   @108   @112
```
### Address Calculation

A cell `T[i]` occupies in memory the number of bytes of its data type.  
Here: `sizeof(int) = 4 bytes`

- **@80** = address of the first byte of cell `T[0]`
- **@84** = @80 + bytes occupied by `T[0]` which is `@80 + (1 × sizeof(int))`
- **@96** = @80 + bytes occupied by `T[0]`, `T[1]`, `T[2]`, `T[3]` which is `@80 + (4 × sizeof(int))`

### Conclusion
The array name + its logical size is sufficient to access all array elements.

</v-clicks>

---

## Using Pointers with Arrays

<v-clicks>

Since an array name is a pointer, we can write:

```c
int* p;
int T[10];
p = T;
```

### Valid Equivalences

| Pointer Notation | Classic Notation | Description |
|------------------------|-------------------|-------------|
| `*(T + i)` | `T[i]` | Access to element i |
| `T + i` | `&T[i]` | Address of element i |
| `scanf("%d", T + i);` | `scanf("%d", &T[i]);` | Input of element i |
| `printf("%d", *(T + i));` | `printf("%d", T[i]);` | Output of element i |

**Note:** `i` is implicitly multiplied by `sizeof(type of T data)`

</v-clicks>

---

## 2D Array Representation with Pointers : In Memory

<v-clicks>

In memory, a 2D array is represented as an **array of arrays**.

```
        M[0]     M[1]     M[2]     ...       M[i]
     ┌────────┬────────┬────────┬────────┬──────────┐
     │  @L0   │  @L1   │  @L2   │  ...   │   @Li    │
     └────────┴────────┴────────┴────────┴──────────┘
        │                                      │
        ▼                                      ▼
    ┌───────┬───────┬───────┐              ┌───────┬───────┬───────┐
@L0 |  [0]  |  [1]  |  ...  |          @Li |  [0]  |  [1]  |  ...  |
    └───────┴───────┴───────┘              └───────┴───────┴───────┘
    Columns                                Columns
```

</v-clicks>

---

## Accessing a 2D Array Cell : Steps

<v-clicks>

To access `M[i][j]` :



```
                                        ① From array M, 
                                        move to cell i
        M[0]     M[1]     M[2]     ...       M[i]
     ┌────────┬────────┬────────┬────────┬──────────┐
     │  @L0   │  @L1   │  @L2   │  ...   │   @Li    │
     └────────┴────────┴────────┴────────┴──────────┘
        │                                      │   ② Get address of row i
        ▼                                      ▼                   M[i][j]
    ┌───────┬───────┬───────┐              ┌───────┬───────┬───────┬─────┐
@L0 |  [0]  |  [1]  |  ...  |          @Li |  [0]  |  [1]  |  ...  | [j] |
    └───────┴───────┴───────┘              └───────┴───────┴───────┴─────┘
    Columns                                Columns
                                        ③ Move to column j
```

</v-clicks>

---

## 2D Array Representation with Pointers : In C Programming

<v-clicks>

Let the 2D array: `int M[3][2];`

### Valid Equivalences

To manipulate a 2D array with pointers:

| Pointer Notation | Classic Notation | Description |
|------------------------|-------------------|-------------|
| `*((*(M+i)) + j)` | `M[i][j]` | Access to element `[i][j]` |
| `(*(M+i)) + j` | `&M[i][j]` | Address of element `[i][j]` |
| `scanf("%d", (*(M+i)) + j);` | `scanf("%d", &M[i][j]);` | Input of element `[i][j]` |
| `printf("%d", *((*(M+i)) + j));` | `printf("%d", M[i][j]);` | Output of element `[i][j]` |

**Note:** `i` and `j` are implicitly multiplied by `sizeof(type of M data)`

</v-clicks>

---
layout: intro
---

# Dynamic Memory Allocation

---

# Memory Space Allocation

<v-clicks>

### Until Now : Static Allocation

Variable declaration automatically reserves the necessary memory space (**static allocation**).

- The number of bytes required is known at **compilation time**
- The compiler calculates this value from the data type of the variable

### BUT...

Often, we must work with data whose size and quantity we cannot predict when writing the program:

- Data size is known at **execution time** only
- We should avoid wasting memory by reserving the maximum possible space

</v-clicks>

---

# Memory Management : Memory Zones

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

### Stack

- Used for initialized/uninitialized declared variables, local variables
- ✅ Memory allocation is **automatic**
- ✅ Memory deallocation is **automatic**
- ✅ Data processing during program **compilation**
- ✅ **Fast** access

</div>

<div>

### Heap

- Used for **dynamic memory allocation**
- ⚠️ Memory allocation is **manual**
- ⚠️ Memory deallocation is **manual**
- ✅ Great **flexibility** in memory management
- ⚠️ Risk of incorrect memory usage
- ⚠️ Requires more **responsibility** from the programmer

</div>

</v-clicks>

</div>

---

# Memory Management : Overview

```
┌──────────────────────────────────────┐
│  Command Line Arguments              │
├──────────────────────────────────────┤
│                                      │
│              Stack ↓                 │  Growth toward bottom
│                                      │
├──────────────────────────────────────┤
│                                      │
│                                      │
├──────────────────────────────────────┤
│                                      │
│              Heap ↑                  │  Growth toward top
│                                      │
├──────────────────────────────────────┤
│      Uninitialized Data              │
├──────────────────────────────────────┤
│       Initialized Data               │
├──────────────────────────────────────┤
│   Program Text / Source Code         │
└──────────────────────────────────────┘
```

---

# Dynamic Allocation : 

<v-clicks>

### Objective
To **reserve or free** memory space as we need it during program **execution**.

### Solution
**Dynamic Memory Allocation**

In C : Using the `malloc` function and the `sizeof` operator

</v-clicks>

---

# Definition : Dynamic Allocation

<v-clicks>

Dynamic memory allocation allows you to manage the memory used by your program "manually".

### Functions from the `stdlib.h` Library

| Function | Description |
|----------|-------------|
| **`malloc()`** | Allocates contiguous bytes and returns the address of the first allocated byte |
| **`calloc()`** | Allocates space for an array initializing its values to zero, and returns the address of the first allocated byte |
| **`free()`** | Frees previously dynamically allocated space |
| **`realloc()`** | Changes the size of previously dynamically allocated space|

</v-clicks>

---

# The `malloc()` Function

<v-clicks>

### For "memory allocation"

The `malloc()` function reserves a memory block of a given size and returns a `void *` pointer (untyped) that can be cast to a pointer of the desired type.

### Syntax

```c
type* ptr = (type*) malloc(size);
```

<div grid="~ cols-3 gap-4">

<div>

`type` : type of the data pointed to by `ptr`

</div>

<div>

`(type*)` : to cast the type of the returned pointer

</div>

<div>

`size` : number of bytes to reserve

</div>

</div>

### ⚠️ Important
If there is insufficient space on your machine, allocation fails and returns **`NULL`** (null pointer).

</v-clicks>

---

## The `malloc()` Function : Generalization for an Array

<v-clicks>

### Generalization for a T array of size N

```c
type* T = (type*) malloc(N * sizeof(type));
```

<div grid="~ cols-4 gap-2">

<div>

`type` : type of the data pointed to by `ptr`

</div>

<div>

`(type*)` : to cast the type of the returned pointer

</div>

<div>

`N` : number of desired array elements

</div>

<div>

`sizeof(type)` : number of bytes a type occupies in memory

</div>

</div>

### Example
```c
int* T = (int*) malloc(10 * sizeof(int));
```

Allocates an array of 10 integers (40 bytes if `sizeof(int) == 4`)

</v-clicks>

---

## The `malloc()` Function : Example 1

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    // declaration of a pointer to an int
    int* A = NULL;
    
    // Allocation of a memory block of 4 bytes
    A = (int*) malloc(4);
    
    printf("Enter an integer : \n");
    scanf("%d", A);
    
    printf("Entered value = %d \n", *A);

    free(A);
    A = NULL;  // Good practice
    
    return 0;
}
```

---

## The `malloc()` Function : Example 2

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int* T = NULL;
    int size;

    printf("Enter the number of values : \n");
    scanf("%d", &size);
    
    T = (int*) malloc(size * sizeof(int)); // allocation of size * 4 bytes
    
    for (int i = 0; i < size; i++) {
        *(T + i) = i + 1;  // initialize values
        printf("T[%d] = %d \n", i, *(T + i)); // display values
    }
    
    free(T);
    T = NULL; 
    return 0;
}
```

---

## The `calloc()` Function

<v-clicks>

### For "contiguous allocation"

The difference between `malloc()` and `calloc()` is that:
- `malloc()` allocates a **single memory block**
- `calloc()` allocates **multiple blocks** all of the same size and **initialized to zero**

### Syntax

```c
type* T = (type*) calloc(N, sizeof(type));
```

<div grid="~ cols-4 gap-2">

<div>

`type` : type of the data pointed to by `T`

</div>

<div>

`(type*)` : to cast the type of the returned pointer

</div>

<div>

`N` : number of desired array elements

</div>

<div>

`sizeof(type)` : size of the type in bytes

</div>

</div>

</v-clicks>

---

## The `calloc()` Function : Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int* T = NULL;
    int size;
    
    printf("Enter the number of values : \n");
    scanf("%d", &size);
    
    T = (int*) calloc(size, sizeof(int)); // allocation of size * 4 bytes
    
    for (int i = 0; i < size; i++) {
        *(T + i) = i + 1;  // initialize values
        printf("T[%d] = %d \n", i, *(T + i)); // display values
    }

    free(T);
    T = NULL;
    
    return 0;
}
```

---

## The `free()` Function

<v-clicks>

Memory space allocated by `calloc()` or `malloc()` is **not automatically freed** → It is necessary to use the `free()` function to free it.

### Syntax
```c
free(T);
```

where `T` is a dynamically allocated pointer

### ⚠️ Important Points

- `free()` frees the space but **doesn't change the pointer's value**
- Remember to set it to `NULL` after calling `free()`
- **Don't** use `free()` to free a static array

### Complete Example
```c
int* T = (int*) malloc(10 * sizeof(int));
// ... usage of T ...
free(T);
T = NULL;  // Good practice
```

</v-clicks>

---

## The `realloc()` Function

<v-clicks>

If previously allocated space proves **insufficient or too large**, you can change its size using `realloc()`.

### Syntax
```c
ptr = realloc(ptr, newsize);
```

<div grid="~ cols-3 gap-2">

<div>

`ptr` : dynamically allocated pointer

</div>

<div>

`newsize` : desired new size

</div>

<div>

Update `ptr` to point to the block whose size was changed

</div>

</div>

### ⚠️ Important
If there isn't enough space after the current block to extend it, a **new block** of the requested size is allocated, then the old block is copied to the new one **and the old block is freed**→ hence the update to `ptr`.

</v-clicks>

---

## The `realloc()` Function : Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int* ptr = NULL;
    int i, n1 = 10, n2 = 20;
    
    ptr = (int*) malloc(n1 * sizeof(int)); // allocation of n1 cells
    
    printf("Address of previously allocated memory: %p\n", ptr);
    
    int* tmp = NULL;
    tmp = realloc(ptr, n2 * sizeof(int)); // reallocation with n2 cells
    if (tmp) {
        ptr = tmp;
        tmp = NULL;
    }
    
    printf("Address of memory after reallocation: %p\n", ptr);
    
    free(ptr);
    ptr = NULL;
    
    return 0;
}
```

---

# Dynamic Allocation of a 2D Array : Steps

<v-clicks>

```
┌─────────────────────────────────┐
│   Address of 2D array M         │  ① First allocate space
├─────────────────────────────────┤     of size nb_lines
│ Address → array line 0          │
├─────────────────────────────────┤
│ Address → array line 1          │
├─────────────────────────────────┤  ② For each line,
│ Address → array line 2          │     allocate space of
├─────────────────────────────────┤     size nb_columns
│           ...                   │
├─────────────────────────────────┤
│ Address → array line i          │─────→  M[i][j] (column j)
└─────────────────────────────────┘
```

### Process in 2 Steps
1. Allocate an array of **pointers** (one cell per line)
2. For each line, allocate an array of the desired size

</v-clicks>

---

# Dynamic Allocation of a 2D Array : C Program

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int** M = NULL;
    int nb_lig = 3;
    int nb_col = 4;
    
    // Allocate space of size nb_lig
    // Each cell is of pointer type
    M = (int**) malloc(nb_lig * sizeof(int*));
    
    // For each line, allocate the number of necessary columns
    // ==> use a loop
    for (int i = 0; i < nb_lig; i++) {
        M[i] = (int*) malloc(nb_col * sizeof(int));
    }
    
    // ... usage of M ...
    
    return 0;
}
```

---

# Applying `free()` to a 2D Array

<v-clicks>

To free space dynamically allocated for a 2D array, one must **free arrays in the reverse order of their allocation**.

### Steps

1. First free the space of **sub arrays** (representing rows)
2. Then, free the space of the **main array** containing their addresses
3. Reset the pointer to `NULL`

### Code

```c
// Free space of small arrays
for(int i = 0; i < nb_lig; i++)
    free(M[i]);

// Free space of main array
free(M);

// Reset pointer to NULL
M = NULL;
```

</v-clicks>

---
layout: intro
---

# Summary

---

## Summary : Pointers and Dynamic Memory Allocation

<v-clicks>

**Pointers**
- A pointer is a variable that contains the address of another variable
- Operator `&` : allows you to get the address of a variable
- Operator `*` : allows you to access the value pointed to by a pointer
- The `*` operator cancels the effect of the `&` operator
- Pointer to pointer : a pointer that points to another pointer

**Dynamic Allocation**
- Dynamic allocation allows you to reserve memory during program execution
- Main functions `malloc()`, `calloc()`, `realloc()` and `free()` are declared in `stdlib.h`
- Always check if dynamic allocation succeeded (pointer not null)
- The number of `free()` calls must match the number of dynamic allocations
- For a 2D array, free lines first, then the main array
- After freeing a pointer, it is recommended to set it to `NULL`

</v-clicks>
