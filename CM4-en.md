---
theme: default
background: #e9e9e9
class: cover
highlighter: shiki
lineNumbers: false
info: |
  ## TI202 - Data Structures and Programming 1
  Lecture 4 - Functions and Modules
transition: slide-left
title: CM4 - Functions and Modules
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

.slidev-content blockquote, .slidev-layout blockquote, blockquote {
  border-left: 10px solid #ff43b8 !important;
  background: #f0f4f8 !important;
  margin-top: 1em !important;
  padding: 1em !important;
  border-radius: 4px !important;
  color: #163767 !important;
}

.two-cols-header {
    column-gap: 20px; /* Adjust the gap size as needed */
}
</style>

# Functions and Modules

TI202 - Data Structures and Programming 1

**Rado Rakotonarivo**  
*Course by Asma Gabis*

---

# Course Outline

<v-clicks>

1. **Functions in C**
    - Categories of functions
    - Prototype, definition, and call
    - Variable scope
2. **Parameter Passing**
    - Review of pass by value and pass by reference
    - Parameter passing in C
    - Passing arrays as parameters
3. **The Notion of Module**
    - Header files (`.h`) 
    - Source files (`.c`)
    - Minimal structure of a modular C project

</v-clicks>

---
layout: intro
---

# Functions in C

---

# Categories of Functions

<v-clicks>

- **Predefined functions** (standard libraries)
- **User-defined functions** (written by the programmer)

</v-clicks>

---

# Predefined Functions

<v-clicks>

- Also called "library functions"
- Examples: `printf()`, `scanf()`, `malloc()`, `free()`
- Usage: include the corresponding `.h` file

```c
#include <stdio.h>
#include <stdlib.h>
```
</v-clicks>

---

# Useful Standard Libraries

<v-clicks>

- `<stdbool.h>`: booleans (`true`, `false`)
- `<string.h>`: string manipulation
- `<math.h>`: mathematical functions
- `<stdlib.h>`: utilities, random numbers

</v-clicks>

---

## Examples of Library Functions

<div grid="~ cols-2 gap-8">

<div>

<v-click>

**Booleans** `<stdbool.h>`: allows use of the `bool` type and the constants `true` and `false` to represent boolean values.
```c
#include <stdbool.h>
```
```c
bool even = true;
```

</v-click>

<v-click>

**Strings** `<string.h>`: provides functions to manipulate strings (arrays of `char` ending with a null character `\0`).
```c
#include <string.h>
```
```c
strlen(word); // length
strcpy(dest, src); // copy
strcat(dest, src); // concatenation
strcmp(s1, s2); // comparison
```
</v-click>

</div>

<div>

<v-click>

**Mathematics** `<math.h>`: provides common mathematical functions.
```c
#include <math.h>
```
```c
pow(x, y); // power
sqrt(x); // square root
```

</v-click>

<v-click>

**Random** `<stdlib.h>`: provides functions for *pseudo* random number generation.
```c
#include <stdlib.h>
```
```c
srand(seed); // initialize the random number generator with a seed
rand(); // random number
```
</v-click>

</div>

</div>

---

# User-defined Functions

<v-clicks>

- Written by the programmer
- Help structure the code
- Two main families:
  - **Void functions** (`void`)
  - **Functions with a return value** (return type)

</v-clicks>

---

# Prototype and Body of a Function

<v-clicks>

- **Prototype**: declaration (signature)
  - Syntax: 
  ```c
  type function_name(type1 param1, type2 param2, ...);
  ```
  - Example:
  ```c
  int sum(int, int);
  ```   

- **Body**: definition
  - Syntax: 
  ```c
  type function_name(type1 param1, type2 param2, ...) {
    // function body
  }
  ```
  - Example:
  ```c
  int sum(int x, int y) {
    return x + y;
  }
  ```
</v-clicks>

---

# Calling a Function

<v-clicks>

- **Arguments** are passed when calling
- Types and order must match the prototype
- Syntax: 
  ```c
  function_name(arg1, arg2, ...);
  ```
- Example:
  ```c
  int res = sum(3, 5);
  ```

</v-clicks>

---

# Where do we write those in the code ?

<v-clicks>

- **Declaration**: before any call to the function
- **Definition**: can be before or after `main()`, but must be declared before any call
- **Call**: a function is called within the definition of another function

### Example:

<div grid="~ cols-2 gap-8">

<div>

```c
#include <stdio.h>

// Function declaration
int sum(int, int);

int main() {
    int res = sum(3, 5); // Function call
    printf("%d\n", res);
    return 0;
}

// Function definition
int sum(int x, int y) {
    return x + y;
}
```
</div>

<div>


```c
#include <stdio.h>

// Declaration and definition
int sum(int x, int y) {
    return x + y;
}

int main() {
    int res = sum(3, 5); // Function call
    printf("%d\n", res);
    return 0;
}
```

> ✅ You can declare and define functions in a different file than where `main()` is located

</div>

</div>

</v-clicks>

---
layout: two-cols-header
---

# Functions With and Without Return Value

::left::

<v-click>

### Functions with Return Value

- Return a value via `return`
- Example:
  ```c
  int sum(int a, int b) {
      return a + b;
  }
  ```

</v-click>

::right::

<v-click>

### Void Functions

- Have `void` as return type
- Do not return any value
- Example:
  ```c
  void print_sum(int a, int b) {
     printf("The sum is %d\n", a + b);
  }
  ```

</v-click>

---

# The 4 Types of Functions

<v-clicks>

| Parameters | Return | Prototype |
|------------|--------|-----------|
| Yes        | Yes    | `type f(type1 param1, ...)` |
| Yes        | No     | `void f(type1 param1, ...)` |
| No         | Yes    | `type f()` |
| No         | No     | `void f()` |

</v-clicks>

---

## Variable Scope: Local vs Global

The **scope** of a variable determines where it is accessible in the code: it is determined by *the block in which it is declared*.

<v-clicks>

- **Local variable**: declared inside a function, accessible only within that function
- **Global variable**: declared outside functions, accessible everywhere

```c
#include <stdio.h>

int N; // global variable

int times_N(int x);

int main() {
    int x = 3; // local variable
    N = 5; // modifies the global variable
    printf("%d\n", times_N(x)); // prints 15
    return 0;
}

int times_N(int x) {
    return N * x; // uses the global variable
}
```
</v-clicks>

---
layout: intro
---

# Parameter Passing

---

## Quick Review from TI102I

<v-clicks>

- *Pass by value/copy*: arguments are copied into parameters, modifications in the function do not affect the caller's variables.
- *Pass by reference*: a reference to the variables is passed, allowing modification of the caller's variables.

<div grid="~ cols-2 gap-8">

<div>
The function

```
function: bad_swap (a: integer, b: integer)
local variables:
  temp: integer
begin
  temp ← a
  a ← b
  b ← temp
end 
```
With a call:
```
x ← 3
y ← 5
bad_swap(x, y)
```

does not modify `x` and `y`.


</div>

<div>
The function

```
function: swap (a: reference integer, 
                b: reference integer)
local variables:
  temp: integer
begin
  temp ← a
  a ← b
  b ← temp
end 
```
With a call:

```
x ← 3
y ← 5
swap(x, y)
```

modifies `x` and `y`.
</div>

</div>

</v-clicks>


---

## In C
<v-clicks>

- There is **only pass by value/copy**.  
- **Pass by reference does not exist in C**. In order to modify variables from the caller, a *pass by copy of the address* is used.

<div grid="~ cols-2 gap-8">

<div>

The function

```c
void bad_swap(int x, int y) {
  int temp = x;
  x = y;
  y = temp;
}
```

With a call:

```c
int a = 3;
int b = 5;
void bad_swap(a, b);
```

does not modify `a` and `b`.

</div>

<div>

The function

```c
void swap(int* x, int* y) {
  int temp = *x;
  *x = *y;
  *y = temp;
}
```

With a call:

```c
int a = 3;
int b = 5;
swap(&a, &b);
```

modifies `a` and `b`.

</div>

</div>

</v-clicks>

---
layout: two-cols-header
---

# What happens in memory?

::left::

<v-clicks>

Recall the `swap` function:

```c
#include <stdio.h>

void swap(int* x, int* y) {
    int temp = *x;
    *x = *y;
    *y = temp;
}

int main() {
    int a = 3;
    int b = 5;
    swap(&a, &b);
    printf("a = %d, b = %d\n", a, b); // prints a = 5, b = 3
    return 0;
}
```

</v-clicks>

::right::

<v-clicks>

Here's what happens in memory:

```plaintext
① Before calling swap
a (main)     b (main)
┌───────┐   ┌───────┐
│   3   │   │   5   │
└───────┘   └───────┘
   @80         @84
② During swap call
x (swap)     y (swap)
┌───────┐   ┌───────┐
│  @80  │   │  @84  │
└───────┘   └───────┘
  @104        @112
③ After swap execution
a (main)     b (main)
┌───────┐   ┌───────┐
│   5   │   │   3   │
└───────┘   └───────┘
   @80         @84
```

</v-clicks>

---

# Passing an Array as a Parameter

<v-clicks>

- Since an array evaluates to the address of its first element, **you can pass an array to a function using a pointer.**
- You **must specify the array size or pass an extra parameter for the size**, as the pointer does not contain this information.
- Two possible syntaxes for declaring an array parameter:
  - `type f(type1* arr, int size)`
  - `type f(type1 arr[], int size)`
- Accessing elements is the same: `arr[i]` or `*(arr + i)`

### Example:

```c
void print_array(int* arr, int size) {
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}
```

</v-clicks>

---
layout: intro
---

# The Notion of Module

---

# What is a Module?

<v-clicks>

- A module is a pair of files:
  - **Source** (`.c`)
  - **Header** (`.h`)
- Using modules helps structure a project into coherent sub-parts
> *Modular programming* is the principle of dividing a program into independent and reusable modules to:
>  - Improve readability
>  - Facilitate maintenance
>  - Encourage code reuse

</v-clicks>

---
layout: two-cols-header
---

## Header File (.h)

::left::

<v-click>

> *Header files* are used to declare the elements of a module that should be accessible from other modules.

A header file can contain:
  - Type declarations
  - Function prototypes
  - Global variables
  - Required includes for the module

As a best practice, it is recommended to use **include guards** to avoid multiple inclusions: *they ensure the header file content is included only once in a source file.*

</v-click>

::right::

<v-click>

### Example Header File

```c {1-2,15|4-6|8-9|11-13|all}{lines:true}
#ifndef FUNCTIONS_H 
#define FUNCTIONS_H

// Required includes
#include <stdio.h>
#include <stdlib.h>

// Constant definitions
#define MAX_SIZE 100

// Function prototypes
int* create_array(int size);
void print_array(int* arr, int size);

#endif // FUNCTIONS_H
```

</v-click>

---

# Source File (.c)

<v-clicks>

> *Source files* contain the function definitions and program logic.

- They **must include the module's header file** so that prototypes and types are known.
- Include a header file with quotes `""` for *local files*, and with angle brackets `< >` for *standard library files*.
  
### Example:

```c
#include "functions.h"

int* create_array(int size) {
    int* arr = (int*)malloc(size * sizeof(int));
    return (arr) ? arr : NULL; // Check allocation
}

void print_array(int* arr, int size) {
    for (int i = 0; i < size; i++) 
        printf("%d ", arr[i]);
    printf("\n");
}
```

</v-clicks>

---

# Minimal Structure of a Modular C Project

<div grid="~ cols-3 gap-4">

<v-clicks>

<div>

**Header File** (`functions.h`)

```c 
#ifndef FUNCTIONS_H 
#define FUNCTIONS_H

#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 100

int* create_array(int size);
void print_array(int* arr, int size);

#endif // FUNCTIONS_H
```
</div>

<div>

**Source File** (`functions.c`)

```c
#include "functions.h"

int* create_array(int size) {
    int* arr = (int*)malloc(size * sizeof(int));
    return (arr) ? arr : NULL; 
}

void print_array(int* arr, int size) {
    for (int i = 0; i < size; i++) 
        printf("%d ", arr[i]);
    printf("\n");
}
```
</div>

<div>

**Main Program** (`main.c`)

```c
#include <stdio.h>
#include <stdlib.h>

#include "functions.h"

int main() {
    int size = 5;
    int* arr = create_array(size);
    if (arr == NULL) {
        printf("Allocation failed\n");
        return 1;
    }
    for (int i = 0; i < size; i++) 
        arr[i] = i + 1; 
    print_array(arr, size);
    free(arr);
    arr = NULL;
    return 0;
}
```
</div>

</v-clicks>

</div>

---
layout: intro
---

# Recap

---

## Key Points to Remember

<v-clicks>

- Functions help structure C code for readability and reusability
- Functions can have parameters and a return value
- Declaration and call syntax must be respected
  ```c
    type function(type1 param1, type2 param2, ...); // prototype
    type function(type1 param1, type2 param2, ...) { 
        // function body
    } // definition
    type result = function(arg1, arg2, ...); // call
  ```

- Variable scope determines accessibility (local vs global)
- In C, parameter passing is by value, but you can simulate pass by reference with pointers
- Modules help organize C projects by separating declarations (header files) from definitions (source files)


</v-clicks>