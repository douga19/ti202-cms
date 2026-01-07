---
theme: default
background: #e9e9e9
layout: cover
highlighter: shiki
lineNumbers: false
info: |
  ## TI202I - Data Structures and Programming 1
  Lecture 1 - Fundamentals
drawings:
  persist: false
transition: slide-left
title: CM1 - C Language Basics
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
  border-left: 4px solid #ff43b8;
  background: #f0f4f8;
  padding: 1rem;
  border-radius: 4px;
  color: #163767;
}
</style>


# C Language Basics

TI202I - Data Structures and Programming 1

**Rado Rakotonarivo**  
*Asma Gabis' Course*

---


# Course Outline

<v-clicks>

1. **Introduction to C Language**

2. **C Language Elements**
   - Variables and Types
   - Operators
   - Type Conversion

3. **Input/Output in C**
   - `printf()` 
   - `scanf()`

4. **Control Structures**
   - Conditionals (`if`, `else`, `switch`)
   - Loops (`while`, `for`, `do-while`)

</v-clicks>

---

# Why the C Language?

<v-clicks>

- 🎯 **Structured language** for multiple purposes
- 📝 **Very concise**: only 32 keywords
- 🔧 **Language of choice** for embedded systems
- ✅ **Stable** and proven
- 🔗 **High-level assembler** - close to the machine
- 🌍 **Highly portable** - works everywhere
- ⚡ **Efficient code** - optimal performance
- 🏗️ **Foundation** for other languages (Perl, Java, Python, PHP...)

</v-clicks>

---

# History of C

<div grid="~ cols-2 gap-8">

<v-click>

### Creation of C

- **Developed by**: Denis Ritchie
- **Location**: Bell Labs
- **Period**: 1972-1973
- **Context**: Development of utilities for Unix

</v-click>

<v-click>

### Evolution

- C remains one of the most used languages
- Fundamental for understanding programming
- ISO C standard
- Still dominant in embedded systems

</v-click>

</div>

---

# Programmer's Jargon

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

### 📄 Source Code
The text of the program you write

```c
int main() {
    printf("Hello World");
    return 0;
}
```

</div>

<div>

### 🔨 Compile (Build)
Transform source code into executable program

```bash
gcc my_program.c -o my_program
```

</div>

<div>

### ⚙️ Executable (Run)
The compiled program that a machine can execute

```bash
./my_program
```

</div>

<div>

### 📚 Library
Predefined functions of the C language

```c
#include <stdio.h>  // stdio = I/O functions
#include <stdlib.h> // stdlib = utility functions
```

</div>

</v-clicks>

</div>

---

# Header Files (.h)

<v-clicks>

- Special files containing function **declarations**
- Extension: `.h` (header)
- Included at the **beginning of source code** with `#include`

**Common examples:**
```c
#include <stdio.h>      // Standard input/output (printf, scanf)
#include <stdlib.h>     // Utility functions
#include <string.h>     // String manipulation
#include <math.h>       // Mathematical functions
```

**Usage:**
```c
#include <stdio.h>

int main() {
    printf("Display on screen\n");
    return 0;
}
```

</v-clicks>

---

# Some C Language Rules

<v-clicks>

### 📋 Mandatory Syntax

- ✅ Every statement **ends with a semicolon** `;`
- ✅ **C is case-sensitive**: `int`, `Int`, `INT` are different
- ✅ **All C keywords are lowercase**: `if`, `while`, `return`
- ✅ **Indentation is important** for readability (ignored by compiler)


### 📝 Special Characters

- `\n` = newline
- `\t` = tab
- `\\` = backslash

</v-clicks>

---

# Process: Compile and Execute

<v-clicks>

```
┌─────────────────┐
│  Source code    │  (my_program.c)<────────┐
│  (what you      │                         |
│   write)        │                         | Syntax errors
└────────┬────────┘                         |
         │ Compilation ─────────────────────┘
         ▼                                  ^
┌─────────────────┐                         |
│   Executable    │  (my_program)           |
│   (compiled     │                         | Semantic errors
│   program)      │                         |
└────────┬────────┘                         |                    
         │ Execution ───────────────────────┘
         ▼
┌─────────────────┐
│     Result      │  (Display, files, etc.)
└─────────────────┘
```

⚠️ To compile and execute a C program, you will need a compiler.

</v-clicks>

---

# 02 - Structure of a C Program

<v-clicks>

```c
#include <stdio.h>

int main() {
    // Variable declaration
    int x = 10;
    
    // Instructions
    printf("The value of x is: %d\n", x);
    
    // Function return
    return 0;
}
```

**Key points:**
- ✅ `#include <stdio.h>` imports I/O functions
- ✅ `main()` is the **required main function**
- ✅ Braces `{}` delimit the **instruction block**
- ✅ `return 0;` indicates successful program termination

</v-clicks>

---

# Comments

<v-clicks>

### Single-line comment
```c
int age; // variable to store age
```

### Multi-line comment
```c
/*
Sum calculation
The user enters two numbers
We perform the addition
*/
int a, b;
int sum;
```

### Purpose of comments
- 📝 Explain the code
- 🎯 Clarify intentions
- 🔄 Make code understandable (for yourself and others)
- 🚫 Comment out code to temporarily disable it

</v-clicks>

---

# Variables and Types

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

- A *variable* is a **name** associated with a **memory location** that contains a **value**.
- Each variable has the following characteristics:
  - A **name** (identifier): to reference it
  - A **type**: defines the nature of the data
  - A **value**: the stored content
  - A **memory address**: where it is stored

```
┌─────────────────────┐
│   variable_name     │  <-- Label (name)
│  ┌───────────────┐  │
│  │      5        │  │  <-- Content (value)
│  └───────────────┘  │
└─────────────────────┘
```

</div>

<div>

- A *type* defines the **nature** of stored data (integer, real, character, etc.).
- A variable of a given type can have **multiple values** of the same type
- But **not multiple different types**
- Each type determines the **memory space** used
- Each type defines the **possible operations**

</div>

</v-clicks>

</div>


---

# Common Types in C

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

### Integer Types

| Type | Meaning |
|------|---------------|
| `char` | Character (1 byte) |
| `int` | Integer (4 bytes) |
| `long` | Long integer (8 bytes) |

**Examples:**
```c
char c = 'A';
int number = 42;
long large_number = 1000000;
```

</div>

<div>

### Real Number Types

| Type | Meaning |
|------|---------------|
| `float` | Single precision real (4 bytes) |
| `double` | Double precision real (8 bytes) |

**Examples:**
```c
float pi = 3.14;
double precision = 3.14159265;
```

</div>

</v-clicks>

</div>

---

# Declaration and Initialization

<v-clicks>

### Declare without initializing
```c
int x;          // Declared, random value
float y;        // Declared, random value
```

### Declare and initialize
```c
int x = 10;                // Defined value: 10
float y = 3.14;            // Defined value: 3.14
char c = 'A';              // Defined value: 'A'
```

### Declare multiple variables
```c
int a, b, c;               // Three integers
int x = 5, y = 10, z = 15; // Three initialized integers
```

### ⚠️ Best Practice
Always **initialize your variables** to avoid unpredictable behavior!

</v-clicks>

---

# Constants

<v-clicks>

- A *constant* is a fixed value that does not change during program execution.
- There are two types of constants in C:
  
  1. **Literal constants**: values directly written in the code
      ```c
       int x = 42;          // 42 is a literal constant
       char c = 'A';       // 'A' is a literal constant
       ```
  2. **User-defined constants**: named values defined with `#define` or `const`
     - Example with `#define`:
       ```c
       #define PI 3.14159
       float circle_area = PI * r * r;
       ```
     - Example with `const`:
       ```c
       const int MAX_SIZE = 100;
       int array[MAX_SIZE];
       ```
#### Convention

Constant names are often written in **UPPERCASE** to distinguish them from variables.

</v-clicks>

---


# Arithmetic Operators

| Operator | Name | Effect | Example | Result |
|-----------|-----|-------|---------|----------|
| `+` | Addition | Adds | `7 + 3` | `10` |
| `-` | Subtraction | Subtracts | `7 - 3` | `4` |
| `*` | Multiplication | Multiplies | `7 * 3` | `21` |
| `/` | Division | Divides | `7 / 3` | `2` (integers) |
| `%` | Modulo | Remainder of division | `7 % 3` | `1` |
| `=` | Assignment | Assigns a value | `x = 5` | `5` |

---

# Assignment: Syntax vs Errors

<v-clicks>

### ✅ Correct

```c
x = 5;           // Assigns 5 to x
a = b = 3;       // Equivalent to: b = 3; a = b;
x = y + z;       // Assigns the sum to x
```

### ❌ Common mistake: Confusing = and ==

```c
if (x = 5)       // ❌ WRONG: assigns 5 to x
if (x == 5)      // ✅ CORRECT: compares x to 5
```

### ❌ Impossibilities

```c
5 = x;           // ❌ ERROR: Cannot assign to a constant
a + b = x;       // ❌ ERROR: Cannot assign to an expression
```

</v-clicks>

---

# Compound Assignment Operators

<v-clicks>

| Operator | Syntax | Equivalent |
|-----------|---------|-----------|
| `+=` | `x += 5` | `x = x + 5` |
| `-=` | `x -= 3` | `x = x - 3` |
| `*=` | `x *= 2` | `x = x * 2` |
| `/=` | `x /= 4` | `x = x / 4` |
| `%=` | `x %= 3` | `x = x % 3` |

### Examples
```c
int x = 10;
x += 5;    // x is 15
x -= 3;    // x is 12
x *= 2;    // x is 24
x /= 4;    // x is 6
```

</v-clicks>

---

# Increment and Decrement

<v-clicks>

### Increment (`++`)
```c
int x = 7;
x++;       // x is 8
++x;       // x is 9
```

### Decrement (`--`)
```c
int x = 7;
x--;       // x is 6
--x;       // x is 5
```

</v-clicks>

---

# Difference: Pre vs Post

<v-clicks>


**Post-increment** `x++`:
- Uses the value **before** incrementing
- Then adds 1

**Pre-increment** `++x`:
- Adds 1 **first**
- Then uses the value

```c
int b, x = 3;
b = x++;    // b = 3, then x = 4
b = ++x;    // x = 4, then b = 4
```

</v-clicks>

---

# Relational Operators (Comparison)

<v-clicks>

| Operator | Name | Effect | Example | Result |
|-----------|-----|-------|---------|----------|
| `==` | Equality | Compares two values | `7 == 3` | `0` (false) |
| `<` | Less than | Strictly less than | `7 < 10` | `1` (true) |
| `<=` | Less or equal | Less than or equal | `7 <= 7` | `1` (true) |
| `>` | Greater than | Strictly greater than | `7 > 3` | `1` (true) |
| `>=` | Greater or equal | Greater than or equal | `7 >= 10` | `0` (false) |
| `!=` | Not equal | Verify difference | `7 != 3` | `1` (true) |

### ⚠️ Important
- Returns `1` if true, `0` if false
- **Do not confuse** `=` (assignment) and `==` (comparison)!

</v-clicks>

---

# Logical Operators

<v-clicks>

| Operator | Name | Syntax | Effect |
|-----------|-----|---------|-------|
| `&&` | Logical AND | `(cond1) && (cond2)` | True if **all** conditions are true |
| `\|\|` | Logical OR | `(cond1) \|\| (cond2)` | True if **at least one** condition is true |
| `!` | Logical NOT | `!(condition)` | Inverts the condition |

### Examples
```c
int age = 25;
if (age >= 18 && age <= 65)
    printf("Working age\n");

if (age < 18 || age > 65)
    printf("Outside working age\n");

int isAdult = (age >= 18) ? 1 : 0;
if (!isAdult)
    printf("Minor\n");
```

</v-clicks>

---

# Characters and Strings

<v-clicks>

### Single character: single quotes
```c
char a = 'A';
char b = 'Z';
char digit = '5';
```

### String: double quotes
```c
char name[] = "Alice";
char course[] = "C Language";
char message[] = "Hello world";
```

### ⚠️ Mind the difference
```c
char c = 'A';       // ✅ Single character
char s[] = "ABC";   // ✅ String
// char x = "A";    // ❌ ERROR: use '' not ""
```

</v-clicks>

---

# Type Conversion (Cast)

<v-clicks>

### Implicit conversion
The compiler automatically converts types (can cause loss)

```c
int x;
double y;
x = 8.324;  // x takes 8 (decimal part lost)
y = 4;      // y takes 4.0 (decimals added)
```

### Explicit conversion (Cast)
Force the desired type in parentheses

```c
int x;
double y;
x = (int) 8.324;         // x = 8
y = (double) 4;          // y = 4.0

printf("x = %d\n", x);
printf("y = %f\n", y);
```

</v-clicks>

---

# Boolean Type in C: Not Native!

<div grid="~ cols-2 gap-4">

<v-click>
<div>

### Solution: Use conventions
```c
// By convention:
// 0 = False
// Any other value = True

int ko = 0;   // False
int ok = 1;      // True
if (ok) {         // Always true
    printf("It's true\n");
}
```
</div>
</v-click>

<v-click>
<div>

### Solution: Create a pseudo-boolean type
```c
#define BOOL int
#define TRUE 1
#define FALSE 0

int main() {
    BOOL check = TRUE;
    if (check) {
        printf("It's true\n");
    }
    return 0;
}
```
</div>
</v-click>

</div>

<v-click>

### Modern solution: `<stdbool.h>`
```c
#include <stdbool.h>
int main() {
    bool check = true;
    if (check) {
        printf("It's true\n");
    }
    return 0;
}
```

</v-click>

---

# 03 - Input/Output in C

<v-clicks>

### `printf()` - Output display
```c
#include <stdio.h>

// in a main()
printf("Hello World!\n");
printf("My age is %d years.\n", 19);
```

### `scanf()` - Read from input
```c
#include <stdio.h>

// in main()
int age;
printf("What is your age? ");
scanf("%d", &age);
printf("You are %d years old.\n", age);
```

`stdio.h` = Header file for Standard Input Output functions

</v-clicks>

---

# `printf()`: Formatted Output

<v-clicks>

```c
printf("message with %d special %f formats", 42, 3.14);
```

### General syntax
- Message in **double quotes**
- `%format` to insert a variable
- Variables enumerated **in order** after the message
- `\n` for newline (not automatic)

### Examples
```c
int age = 25;
float price = 19.99;
char name[] = "Alice";

printf("Age: %d years\n", age);
printf("Price: %f€\n", price);
printf("Name: %s\n", name);
printf("%d * %f = %f\n", age, price, age * price);
```

</v-clicks>

---

# `printf()` Formats

<v-clicks>

| Format | Type | Example |
|--------|------|---------|
| `%d` | Integer (int) | `printf("%d", 42)` |
| `%ld` | Long integer (long) | `printf("%ld", 1000000)` |
| `%f` | Real (float) | `printf("%f", 3.14)` |
| `%lf` | Double real (double) | `printf("%lf", 3.14159)` |
| `%c` | Character (char) | `printf("%c", 'A')` |
| `%s` | String | `printf("%s", "Hello")` |
| `%x` | Hexadecimal | `printf("%x", 255)` |
| `%e` | Scientific notation | `printf("%e", 1000.0)` |

### Precision specifiers
```c
printf("%.2f€\n", 19.9999);  // 19.99€
printf("%5d\n", 42);          // "   42" (5 characters)
printf("%-5d\n", 42);         // "42   " (left aligned)
```

</v-clicks>

---

# `scanf()`: Reading Data

<v-clicks>

```c
#include <stdio.h>

int main() {
    int age;
    float price;
    
    printf("What is your age? ");
    scanf("%d", &age);
    
    printf("What is the price? ");
    scanf("%f", &price);
    
    printf("You are %d years old and the price is %.2f€\n", age, price);
    return 0;
}
```

### Important points
- The `&` operator gives the **memory address** (except for strings)
- Variables must be **preceded by &** (address)
- Strings `char[]` **do not need &**

</v-clicks>

---

# `scanf()`: Examples

<v-clicks>

```c
// Read ONE CHARACTER
char nextChar;
scanf("%c", &nextChar);

// Read ONE REAL NUMBER
float radius;
scanf("%f", &radius);

// Read TWO INTEGERS (separated by space)
int length, width;
scanf("%d %d", &length, &width);

// Read TWO INTEGERS (separated by semicolon)
int length, width;
scanf("%d;%d", &length, &width);

// Read A STRING (without &)
char name[50];
scanf("%s", name);  // No & for strings!
```

</v-clicks>

---

# 04 - Control Structures

<v-clicks>

Control structures allow you to:
- **Make choices** based on conditions
- **Repeat** instruction blocks

### Two main types

**Conditional structures:**
- `if` / `else`
- `switch` / `case`

**Loops:**
- `for`
- `while`
- `do-while`

</v-clicks>

---

# The if Statement

<v-clicks>

```c
if (condition) {
    // Actions executed if condition is TRUE
    instruction1;
    instruction2;
}
```

### Syntax
- Parentheses around the condition are **mandatory**
- Braces delimit the block (recommended even for single instruction)
- Condition: comparison or logical expression

### Example
```c
int age = 25;
if (age >= 18) {
    printf("You are an adult\n");
}
```

</v-clicks>

---

# The if-else Statement

<v-clicks>

```c
if (condition) {
    // Actions if condition TRUE
} else {
    // Actions if condition FALSE
}
```

### Example
```c
int delta = -5;
if (delta >= 0) {
    printf("There exists one or two solutions\n");
} else {
    printf("No real solution\n");
}
```

</v-clicks>

---

# Nested if Statements

<v-clicks>

```c
int month = 3;

if (month == 1) {
    printf("January\n");
} else if (month == 2) {
    printf("February\n");
} else if (month == 3) {
    printf("March\n");
} else {
    printf("Other month\n");
}
```

### ⚠️ Warning
This style becomes **hard to read** with many cases  
→ Use `switch-case` instead!

</v-clicks>

---

# The switch-case Statement

<v-clicks>

```c
switch (variable) {
    case value1:
        instructions;
        break;
    case value2:
        instructions;
        break;
    default:
        instructions for default case;
}
```

### Example
```c
int month = 1;
switch (month) {
    case 1:
        printf("January\n");
        break;
    case 2:
        printf("February\n");
        break;
    default:
        printf("Other month\n");
}
```

</v-clicks>

---

# Loops: Concepts

<v-clicks>

A loop executes an instruction block **multiple times**

### Three types of loops

**for:**
- When you **know** the number of repetitions (iterations)
- Classic for traversing an interval

**while:**
- When you **don't know** the number of iterations
- You have a stop condition

**do-while:**
- Like while but executes **at least once**

</v-clicks>

---

# The for Loop

<v-clicks>

```c
for (initialization; condition; increment) {
    actions;
}
```

### Simple example
```c
for (int x = 0; x < 10; x++) {
    printf("%d ", x);
}
// Displays: 0 1 2 3 4 5 6 7 8 9
```

### Breakdown
```c
for (int i = 1; i <= 5; i++) {
    printf("Iteration %d\n", i);
}
// i = 1 → display → i++ (i = 2)
// i = 2 → display → i++ (i = 3)
// ...until i = 6 (condition false, stop)
```

</v-clicks>

---

# The while Loop


When you **don't know in advance** how many times to repeat

```c
initialization;
while (condition) {
    actions;
    increment;
}
```

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

### Example 1: Like a `for`
```c
int x = 0;
while (x < 10) {
    printf("%d ", x);
    x++;
}
// Displays: 0 1 2 3 4 5 6 7 8 9
```

</div>

<div>

### Example 2: Input validation

```c
int number;
printf("Enter a positive number: ");
scanf("%d", &number);

while (number < 0) {
    printf("Invalid number, try again: ");
    scanf("%d", &number);
}
printf("You entered %d\n", number);
// Continues until a positive number is entered
```
</div>

</v-clicks>

</div>


---

# The do-while Loop

<v-clicks>

```c
do {
    actions;
    increment;
} while (condition);
```

### Major difference with `while`
- **Executed at least once** even if condition is false
- Condition is checked at the **end** of each iteration

### Example
```c
int x = 0;
do {
    printf("%d ", x);
    x++;
} while (x < 10);
// Same result as for and while
```

### Use cases
- Interactive menu where you want to display at least once
- Input validation with at least one attempt

</v-clicks>

---

# `break` and `continue`

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

### `break`
- **Immediately** exit a loop or switch block
- Executes the instruction after the loop

```c
for (int i = 0; i < 10; i++)
{
    if (i == 5)
        break;  // Exit the loop
    printf("%d ", i);
}
// Displays: 0 1 2 3 4
```
</div>

<div>

### `continue`
- Skip to the **next iteration**
- The condition is reevaluated

```c
for (int i = 0; i < 10; i++)
{
    if (i == 5)
        continue;  // Skip to i=6
    printf("%d ", i);
}
// Displays: 0 1 2 3 4 6 7 8 9
```
</div>

</v-clicks>

</div>

---

# Comparison: for, while, do-while

<div grid="~ cols-3 gap-2">

<v-clicks>

<div>

### for
```c
for (int i = 0; 
     i < 10; 
     i++)
{
    printf("%d ", i);
}
```

- Number of iterations known
- Concise
- Classic

</div>

<div>

### while
```c
int i = 0;
while (i < 10)
{
    printf("%d ", i);
    i++;
}
```

- Number of iterations unknown
- More flexible
- Condition at start

</div>

<div>

### do-while
```c
int i = 0;
do
{
    printf("%d ", i);
    i++;
} while (i < 10);
```

- At least once
- Less common
- Condition at end

</div>

</v-clicks>

</div>

---
