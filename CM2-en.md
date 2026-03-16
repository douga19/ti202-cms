---
theme: default
background: #e9e9e9
class: cover
highlighter: shiki
lineNumbers: false
info: |
  ## TI202I - Data Structures and Programming 1
  Lecture 2 - Arrays and Strings
drawings:
  persist: false
transition: slide-left
title: CM2 - Arrays and Strings
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
    column-gap: 20px;
}
</style>

# Arrays and Strings

TI202I - Data Structures and Programming 1

**Rado Rakotonarivo**  
*Course by Asma Gabis*

---

# Course Outline

<v-clicks>

1. **1D Arrays**
   - Declaration and initialization
   - Array manipulation

2. **Sorting Algorithms**
   - Bubble sort
   - Selection sort

3. **Binary Search**

4. **2D Arrays**
   - Matrix manipulation

5. **Strings**
   - Declaration and manipulation

</v-clicks>

---
layout: intro
---

# 1D Arrays

---

# Basic Idea: Reminder

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

### Initial Problem
Example: 7 numeric variables representing a student's grades

```c
int note1;
int note2;
int note3;
int note4;
int note5;
int note6;
int note7;
```

</div>

<div>

### Solution: The Array
Group the information into a single container called an **array**

```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│  0  │  1  │  2  │  3  │  4  │  5  │  6  │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│val1 │val2 │val3 │val4 │val5 │val6 │val7 │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┘
```

**Equivalence:**
```c
note1 = val1;  // becomes  Notes[0] = val1;
note4 = val4;  // becomes  Notes[3] = val4;
```

</div>

</v-clicks>

</div>

<v-click>

### ⚠️ Key Points
- Each cell has an **index**
- Indices **always start from 0**
- Number of cells = array size
- **Cell content** = value
- **Index** (from 0) = position of the value

</v-click>

---

# Array Size: Reminder

<v-clicks>

An array is characterized by two different sizes:

### 📦 Physical size
- Number of cells **reserved** in memory
- Defined at array declaration
- Cannot be changed

### 📝 Logical size
- Number of cells **filled** with meaningful values
- Can be different from the physical size
- Changes during program execution

### ⚠️ Important
Each array must be associated with an **additional variable** containing its logical size

```c
int array[100];  // Physical size = 100
int n = 10;  // Only 10 cells used
```

</v-clicks>

---

# Declaring an Array in C
<v-clicks>

### General Syntax
```c
Type ArrayName[physical_size];
```

- **Type**: indicates the type of data to store in the array
- **physical_size**: MUST be a constant value/expression
### Examples
```c
int arr[10];            // Array for up to 10 integers
float myArray[3284];   // Array for up to 3284 floats

// With a defined constant
#define SIZE 10
int values[SIZE];    // Size defined by a constant
```

### Multiple Declarations
```c
Type Arr1[size1], Arr2[size2], ...;

int b[100], x[27];     // Two integer arrays
```

</v-clicks>

---

# Array Initialization

<v-clicks>

### Initialization with implicit size
```c
// Empty brackets and values in braces
// Physical size = logical size = number of values
int n[] = {1, 2, 3, 4, 5};
```

### Initialization with explicit size
```c
int m[5] = {1, 2, 3, 4, 5};     // Size = number of values
int k[8] = {1, 2, 3};            // The rest is initialized to zero
int z[5] = {0};                  // All elements to zero
```

### ⚠️ Important rules
- If **physical size > number of values** → the rest of the array is initialized to zero
- If **physical size < number of values** → syntax error

</v-clicks>

---

# Accessing Array Elements

<v-clicks>

Access an array element using the **array name** and the **position** of the element in brackets.

### Syntax
```c
ArrayName[element_index]
```

### Example
```c
#include <stdio.h>

int main() {
    int primes[] = {2, 3, 5, 7, 11, 13, 17, 19};
    
    // Note: this is the 4th value in the list
    printf("Value at index 3: %d.\n", primes[3]);
    // Prints: 7
    
    // Because numbering starts from 0
    printf("The 5th value in this list: %d.\n", primes[4]);
    // Prints: 11
    
    return 0;
}
```

</v-clicks>

---

# Filling an Array

<v-clicks>

### Two necessary steps

1. **Determine the logical size** (fixed or entered by the user) ≤ physical size
2. **Fill the elements** one by one → use a loop

### Complete example
```c
#include <stdio.h>

int main() {
    int arr[20];
    int n = 10;
    
    // Enter 10 integers
    printf("Enter %d integers: \n", n);
    
    // Loop to enter values one by one
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);  // Each cell is entered like a variable
    }
    
    return 0;
}
```

</v-clicks>

---

# Displaying Array Elements

<v-clicks>

Array elements must be **displayed one by one** (unlike strings).

### Example
```c
#include <stdio.h>

int main() {
    int arr[] = {2, 12, 34, 11, 8};
    int n = 5;
    
    // Display array elements
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);  // Separate values with spaces
    }
    printf("\n");
    
    return 0;
}
```

**Result:**
```
2 12 34 11 8
```

</v-clicks>

---

# Things to avoid with Arrays

<v-clicks>

### ❌ Non-constant physical size | Even though some compilers may accept it
```c
int n;
...
int T[n];      // Don't do this (even if it may compile)
int T[2*n];    // Don't do this
```

### ❌ Reading elements one at once
```c
int T[10];
scanf("%d", T);  // Don't do this, fill element by element (loop)
```

### ❌ Displaying an array one at once
```c
printf("%d", T);  // Don't do this, display element by element (loop)
```

</v-clicks>

---

# More Errors to Avoid

<v-clicks>

### ❌ Negative index and `len()` function
```c
int T[10];
T[-1] = 0;     // Don't do this
n = len(T);    // Don't do this, can't get array size
```

### ❌ Comparing two arrays
```c
int T1[10], T2[10];
...
if (T1 == T2)  // Don't do this
    ...
```

You must compare the content **element by element** with a loop:
```c
int equal = 1;  // Hypothesis: arrays are equal
for (int i = 0; i < size; i++) {
    if (T1[i] != T2[i]) {
        equal = 0;  // Difference found
        break;
    }
}
```

</v-clicks>

---
layout: intro
---

# Sorting Algorithms

---

# Sorting an Array: Definition

<v-clicks>

### What is a sorting algorithm?

A sorting algorithm **organizes the elements** of an array in a given order:
- **Ascending**: from smallest to largest
- **Descending**: from largest to smallest

### Main objective
Make **searching** in an array easier

### Why several algorithms?
- Looking for the most **optimal** in terms of operations
- Comparisons, swaps, etc.
- Different strategies for different use cases

### Examples of sorting algorithms
- Bubble sort
- Insertion sort
- Selection sort
- And many others...

</v-clicks>

---

# Bubble Sort: Principle

<v-clicks>

One of the simplest sorting algorithms.

### How it works

1. Go through the array from start to end
2. Compare the values of two consecutive cells
3. If the values are not in the desired order, swap them
4. Continue the process until the array is completely sorted

### In other words
- After one iteration of the outer loop, the **maximum value** is at the end of the array
- The inner loop should only iterate over unsorted elements

</v-clicks>

---
layout: two-cols-header
---

# Bubble Sort: C Implementation

::left::

### C Program
```c
#include <stdio.h>
#define SIZE 100

int main() {
    int A[SIZE] = {13, 7, 43, 5, 3, 19, 2, 23, 29};
    int n = 9, i, j, temp;  

    for (i = 0; i < n - 1; i++) {
        for (j = 0; j < n - 1 - i; j++) {
            if (A[j] > A[j + 1]) {
                temp = A[j];
                A[j] = A[j + 1];
                A[j + 1] = temp;
            }
        }
    }  
    return 0;
}
```

::right::

### Variable Correspondence

In the program:

- `i`: index for the outer loop (iterations)
- `j`: index for the inner loop (comparisons)
- `temp`: temporary variable for swapping

### Visualization

Find an interactive animation of the bubble sort algorithm on [Visualgo](https://visualgo.net/en/sorting)

---
layout: iframe
url: https://visualgo.net/en/sorting
---

# Bubble Sort: Example

---

# ⚠️ Efficiency Problem!

<v-click>

The algorithm keeps running and checking values even though the array is sorted by the 6th iteration.

**How can we improve it?**

</v-click>

---

# Selection Sort: Principle

<v-clicks>

Another sorting algorithm, often more efficient than bubble sort.

### Principle (for ascending sort)

1. Find the **minimum** value in the array (get its position)
2. Swap it with the **first value** of the array → The minimum is now in its final position
3. Consider the unsorted zone and repeat the previous two steps

### In other words
- Divide the array into two zones: sorted and unsorted
- At each iteration, extract the minimum from the unsorted zone and place it at the end of the sorted zone
- At each iteration, the size of the sorted zone increases by 1 and the unsorted zone decreases by 1

</v-clicks>

---
layout: two-cols-header
---

## Selection Sort: C Implementation

::left::

### C Program

```c
#include <stdio.h>
#define SIZE 100

int main() {

    int A[SIZE] = {13, 7, 43, 5, 3, 19, 2, 23, 29};
    int n = 9, i, j, temp, min;

    for (i = 0; i < n - 1; i++) {
        min = i;     
        for (j = i + 1; j < n; j++) {
            if (A[j] < A[min]) {
                min = j;
            }
        }    
        if (min != i) {
            temp = A[i];
            A[i] = A[min];
            A[min] = temp;
        }
    } 
    return 0;
}
```

::right::

### Variable Correspondence

In the program:

- `i`: index for the sorted zone
- `j`: index for the unsorted zone
- `min`: index of the minimum value found (in the unsorted zone)
- `temp`: temporary variable for swapping

### Visualization

Find an interactive animation of the selection sort algorithm on [Visualgo](https://visualgo.net/en/sorting)

---
layout: iframe
url: https://visualgo.net/en/sorting
---

# Selection Sort: Example

---
layout: intro
---

# Binary Search

---

# Binary Search: Principle

<v-clicks>

### Prerequisite
⚠️ Applied **only** to a **sorted** array

### Algorithm principle
At each step:

1. **Split** the array `A` into two subarrays using a median index `m`
   - Lower half
   - Upper half

2. Use **2 indices**: left `l` and right `r`
   - Calculate the median index `m = (l + r) / 2`
   - Or `m = l + (r - l) / 2` to avoid overflow

3. **Compare** the value at the median index `m` to the searched value:
   - If the searched value is **equal** to `A[m]`, the search is over
   - If the searched value is **greater or equal** to `A[m]`, search again in the **upper half**
   - Otherwise, search again in the **lower half**

</v-clicks>

---
layout: two-cols-header
---

::left::

### C Program

```c
#include <stdio.h>
#define SIZE 100
int main() {
    int A[SIZE] = {1, 1, 2, 3, 5, 8, 13, 21, 34, 55};
    int m, n = 10, found = 0;
    int value = 21; 
    int l = 0;
    int r = n - 1;     
    
    while (l <= r && !found) {
        m = l + (r - l) / 2;       
        if (A[m] == value) {
            found = 1;         
        } else if (value > A[m]) {
            l = m + 1;          
        } else {
            r = m - 1;          
        }
    }
    if (found) {
        printf("Value found at index %d\n", m);
    } else {
        printf("Value not found\n");
    }
    return 0;
}
```

::right::

### Comments

In the program:
- `l`: start of the search zone
- `r`: end of the search zone
- `m`: median index
- `found`: search success indicator (1 if found, 0 otherwise)
- `l = m + 1`: reduces the search zone to the upper half
- `r = m - 1`: reduces the search zone to the lower half

### Visualization

Find an interactive animation of binary search [here](https://www.mathwarehouse.com/programming/gifs/binary-vs-linear-search.php)

---
layout: iframe
url: https://www.mathwarehouse.com/programming/gifs/binary-vs-linear-search.php
---

# Binary Search: Example

---

# Binary Search: Notes

<v-clicks>

### Advantages

- ⚡ **Very fast** for large arrays
- 📉 Logarithmic complexity O(log n) 
- 🎯 Much more efficient than sequential search 

### Disadvantage

- ⚠️ **Requires a sorted array** beforehand

</v-clicks>

---
layout: intro
---

# 2D Arrays

---

## General Representation: Reminder

<v-clicks>

A 2D array is a data structure organized in **rows** and **columns** (matrix).

```
                Columns
            j=0   j=1   j=2
           ┌─────┬─────┬─────┐
       i=0 │val1 │val2 │val3 │
           ├─────┼─────┼─────┤
       i=1 │val4 │val5 │val6 │
           ├─────┼─────┼─────┤
Rows   i=2 │val7 │val8 │val9 │
           ├─────┼─────┼─────┤
       i=3 │val10│val11│val12│
           └─────┴─────┴─────┘
```

</v-clicks>

---

# Declaring a 2D Array

<v-clicks>

### Syntax
```c
Type MatName[MAX_ROWS][MAX_COLS];
```

- **MAX_ROWS**: Maximum reserved rows (Physical size rows)
- **MAX_COLS**: Maximum reserved columns (Physical size columns)

### Examples
```c
#include <stdio.h>
#define NB_ROWS 20
#define NB_COLS 10

int main() {
    int M1[100][100];           // 100x100 matrix
    int M2[NB_ROWS][NB_COLS];   // 20x10 matrix
    
    return 0;
}
```

</v-clicks>

---

# Initializing a 2D Array

<v-clicks>

### Sequential initialization
```c
// Sequential initialization of the matrix
int M[3][4] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11};
```

Memory result:
```
┌───┬───┬───┬────┐
│ 0 │ 1 │ 2 │  3 │
├───┼───┼───┼────┤
│ 4 │ 5 │ 6 │  7 │
├───┼───┼───┼────┤
│ 8 │ 9 │10 │ 11 │
└───┴───┴───┴────┘
```

### Row-wise initialization
```c
int M[3][4] = {
    {0, 1, 2, 3},
    {4, 5, 6, 7},
    {8, 9, 10, 11}
};
```

</v-clicks>

---

# Accessing a 2D Array Cell

<v-clicks>

To access a cell, **two indices** are needed.

### Syntax
```c
MatName[row_index][col_index]
```

### Examples
```c
int M1[100][100];
int M2[NB_ROWS][NB_COLS];

// Enter value at (0, 0)
scanf("%d", &M1[0][0]);

// Display value at (0, 1)
printf("%d", M2[0][1]);

// Modify a value
M1[2][3] = 42;
```

</v-clicks>

---

# Filling a 2D Array

<v-clicks>

To fill a 2D array, use **two nested loops**:
- One for **rows**
- One for **columns**

### Complete example
```c
#include <stdio.h>
#define NB_ROWS 20
#define NB_COLS 10

int main() {
    int M1[NB_ROWS][NB_COLS];
    int i, j, rows = 3, cols = 4;
    
    for (i = 0; i < rows; i++) {           // Loop over rows
        for (j = 0; j < cols; j++) {       // Loop over columns
            printf("Enter a value: ");
            scanf("%d", &M1[i][j]);
        }
    }
    
    return 0;
}
```

</v-clicks>

---

# Displaying a 2D Array

<v-clicks>

To display a 2D array in a readable way, use **two nested loops** with a line break after each row.

### Complete example
```c
#include <stdio.h>
#define NB_ROWS 20
#define NB_COLS 10

int main() {
    // Sequential initialization of the matrix
    int M[3][4] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11};
    int i, j, rows = 3, cols = 4;
    
    for (i = 0; i < rows; i++) {
        for (j = 0; j < cols; j++) {
            // Separate values in the same row by 2 tabs
            printf("%d\t\t", M[i][j]);
        }
        // Line break before displaying the next row
        printf("\n");
    }
    
    return 0;
}
```

**Result:**
```
0       1       2       3
4       5       6       7
8       9       10      11
```

</v-clicks>

---
layout: intro
---

# Strings

---

# Strings: Definition

<v-clicks>

A **string** is defined as a **1D array of characters** ending with the character `\0`.

### End character `\0`
- Visually composed of **two characters** (`\` and `0`)
- But represents **a single character** (null character)
- Marks the **end of the string**

### Declaration
```c
char StringName[physical_size];
```

### Important
```
Array size = number of characters + 1 ('\0')
```

</v-clicks>

---

# Declaration and Initialization

<v-clicks>

### Method 1: Character array
```c
// Character array + '\0' = string
char greeting[6] = {'H', 'E', 'L', 'L', 'O', '\0'};
```

### Method 2: Direct assignment (recommended)
```c
// The C compiler automatically adds the '\0' character
char salutation[] = "Hello";
```

Both methods are equivalent, but the second is simpler and the compiler adds `\0` automatically.

</v-clicks>

---

# Memory Representation

<v-clicks>

```c
char salutation[] = "Hello";
```

Memory representation:

```
┌───┬───┬───┬───┬───┬────┐
│'H'│'e'│'l'│'l'│'o'│'\0'│
└───┴───┴───┴───┴───┴────┘
  0   1   2   3   4    5
  ↑
Index
```

### Key points
- Each character is accessed by **index**
- Indices start at **0**
- The `\0` character occupies one cell (index 5)
- The physical size is **6** to store "Hello" (5 letters + 1 for `\0`)

</v-clicks>

---

# Displaying a String

<v-clicks>

It is displayed **in block** with the `%s` format (unlike arrays).

### Examples
```c
char greeting[6] = {'H', 'E', 'L', 'L', 'O', '\0'};
char salutation[] = "Hello";

printf("%s", salutation);  // Prints: Hello
printf("%s", greeting);    // Prints: HELLO
```

### Accessing an individual character

Access is done directly by index with the `%c` format:

```c
printf("%c", salutation[0]);  // Prints: H
printf("%c", salutation[1]);  // Prints: e
printf("%c", salutation[4]);  // Prints: o
```

</v-clicks>

---

# Reading a String from Input

<v-clicks>

Input is done **in block** with the `%s` format.

### Syntax
```c
char My_str[32];
scanf("%s", My_str);
```

### ⚠️ Important
- **No `&`** for string input
- Unlike other types (`int`, `float`, etc.) which require `&`

### Complete example
```c
#include <stdio.h>

int main() {
    char name[50];
    printf("Enter your name: ");
    scanf("%s", name);  // No &
    printf("Hello %s!\n", name);
    return 0;
}
```

</v-clicks>

---

# Reading a Sentence from Input: ❌ `scanf()`

<v-clicks>

### Definition
A sentence = a sequence of words separated by **spaces**

### Problem with `scanf`

```c
#include <stdio.h>
#define LEN 100

int main() {
    char str[LEN];
    printf("Enter a string: \n");
    scanf("%s", str);
    printf("%s \n", str);
    return 0;
}
```

**User input:** `Hello world everyone`

**Result:** `Hello`

❌ The string `str` is incomplete: `scanf` stops at the **first space encountered**!

</v-clicks>

---
layout: two-cols-header
---

## Solution: Using `fgets`

::left::

<v-clicks>

### Description

- `fgets` allows you to read a complete line from the standard input (`stdin`), including spaces, and stores the read characters in a string.
- This function reads up to the newline character `\n` or up to the specified maximum size.

### Syntax

```c
fgets(string_name, max_size, stdin);
// stdin: standard input (keyboard)
// stdin is a predefined variable in <stdio.h>
```

</v-clicks>


::right::

<v-clicks>

### Complete example

```c
#include <stdio.h>
#define LEN 100

int main() {
    char str[LEN];
    printf("Enter a string: \n");
    fgets(str, LEN, stdin);  // Read a complete line
    printf("%s", str);
    return 0;
}
```

**User input:** `Hello world everyone`

**Result:** `Hello world everyone`

</v-clicks>


---

## Arrays VS Strings

| Characteristic | Array | String |
|----------------|---------|---------------------|
| **Display** | element by element → loop | In block with `%s` |
| **Input** | element by element → loop | In block with `%s` |
| **Scanf** | Formats `%d`, `%f`, `%c`... requiring `&` | Format `%s` **without** `&` |
| **Stop condition** | Logical size | The `\0` character |
| **Element access** | By index `T[i]` | By index `str[i]` |

---

## Comparative Example

```c
// Integer array
int tab[10];
for (int i = 0; i < 10; i++) scanf("%d", &tab[i]);  // With &
for (int i = 0; i < 10; i++) printf("%d ", tab[i]);  // element by element

// String
char str[50];
scanf("%s", str);      // Without &
printf("%s", str);     // In block
```
