---
theme: default
background: #e9e9e9
class: cover
highlighter: shiki
lineNumbers: false
info: |
  ## TI202 - Data Structures and Programming 1
  Lecture 5 - Types and Structures
transition: slide-left
title: CM5 - Types and Structures
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
  margin-bottom: 1em !important;
  padding: 1em !important;
  border-radius: 4px !important;
  color: #163767 !important;
}

.two-cols-header {
    column-gap: 20px; /* Adjust the gap size as needed */
}
</style>

# Types & Structures

TI202 - Data Structures and Programming 1

**Rado Rakotonarivo**  
*Course by Asma Gabis*

---

# Course Outline

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

1. **Type definition and redefinition**
    - The `typedef` keyword
    - Type redefinition examples

2. **Enumerations**
    - Definition and syntax
    - Usage example
    - Enumeration values

</div>

<div>

3. **Structures and structured types**
    - Definition and syntax
    - Initialization and field access
    - Pointer to a structure
    - Memory representation and usage
    - Structure composition
    - Arrays of structures
    - Structures as function parameters

</div>

</v-clicks>

</div>

---
layout: intro
---

# Type definition and redefinition

---

# The `typedef` keyword

<v-clicks>

## Why?

- Create your own types from base types
- Improve code readability
    - Example: Define a `bool` type from `int` to represent boolean values
- Allow minor modifications for code generalization
    - Example: Change the type of an item array from `double` to `int` by modifying a single line

## How?

- The `typedef` keyword creates an *alias* for an existing type (redefines an existing type)
- Syntax:
   ```c
   typedef existing_type t_new_type;
  ```

> By convention, user-defined types are prefixed with `t_`. For example: `t_int`, `t_string`, `t_date`, etc.

</v-clicks>

---

# Type redefinition examples

<v-clicks>

Redefining `int` as `t_int` and `char*` as `t_string`:
```c
typedef int t_int;
typedef char* t_string;
```

allows you to use these new types in code more expressively:
```c
t_int x = 42;
printf("%d", x);

t_string course = "programming";
printf("%s", course);
```

</v-clicks>

---

# Type redefinition examples

<v-clicks>

Redefining `int` as `t_int` and `char*` as `t_string`:
```c
typedef int t_int;
typedef char* t_string;
```

allows you to use these new types in code more expressively:
```c
t_int x = 42;
printf("%d", x);

t_string course = "programming";
printf("%s", course);
```

</v-clicks>

---

# Type redefinition examples

<v-clicks>

The `sizeof` operator works with new types:

```c
typedef double t_item;

t_item* tab = (t_item*) malloc (10 * sizeof(t_item)); // Dynamic allocation of an array of 10 doubles
```

By changing only the type redefinition line, you can change the type of the array elements without modifying the rest of the code:

```c
// Change double to int:
typedef int t_item;

t_item* tab = (t_item*) malloc (10 * sizeof(t_item)); // Dynamic allocation of an array of 10 integers
```

</v-clicks>

---

# Where to define new types?

> - New types are generally defined in header files (`.h`)
> - The rule remains: before using a new type in a source file (`.c`), it must be defined beforehand, either in the same source file or in a header file included in that source file

<div grid="~ cols-[1fr_2fr] gap-4">

<v-clicks>

<div>

### Header file `items.h`

```c
#ifndef ITEMS_H
#define ITEMS_H

#include <stdlib.h>
// Redefine double as t_item
typedef double t_item;

t_item* new_items_array(int size);
void free_items_array(t_item* items);

#endif // ITEMS_H
```
</div>

<div>

### Source file `items.c`

```c
#include "items.h"

t_item* new_items_array(int size) {
    t_item* items = (t_item*) malloc(size * sizeof(t_item));
    return items;
}

void free_items_array(t_item* items) {
    free(items);
}
```

</div>

</v-clicks>

</div>

---
layout: intro
---

# Enumerated types

---

## Definition

- An *enumerated type* or *enumeration* is a list of possible values for a variable
- To make code more readable, you can associate names with these values, for example to represent days of the week, colors, priority levels, etc.

<v-clicks>

## Syntax

<div grid="~ cols-3 gap-4">

<div>

*Option 1 (named enum then redefinition)*
```c
enum e_enum_name { 
    ELEMENT1,
    ELEMENT2, 
    ELEMENT3, 
    ... 
};
typedef enum e_enum_name t_enum_name;
```

</div>


<div>

*Option 2 (unnamed enum directly redefined)*
```c
typedef enum { 
    ELEMENT1, 
    ELEMENT2, 
    ELEMENT3, 
    ... 
} t_enum_type_name;
```

</div>

<div>

*Option 3 (named enum directly redefined)*
```c
typedef enum e_enum_name { 
    ELEMENT1, 
    ELEMENT2, 
    ELEMENT3, 
    ... 
} t_enum_type_name;
```
</div>

</div>

> By convention, enumeration names are prefixed with `e_` and enumeration elements are written in UPPERCASE.

</v-clicks>

---

# Example

<div grid="~ cols-[1fr_2fr] gap-4">

<v-clicks>

<div>

```c
#include <stdio.h>

typedef enum { OK, WARNING, ERROR } t_status;

int main() {
    t_status s = OK;
    if (s == OK) {
        printf("Status is OK\n");
    } else if (s == WARNING) {
        printf("Status is WARNING\n");
    } else if (s == ERROR) {
        printf("Status is ERROR\n");
    }
    return 0;
}
```

</div>

<div>

- In this example, we follow option 2 syntax to define an unnamed enumeration and directly redefine it as `t_status`.
- `enum { OK, WARNING, ERROR }` is an *unnamed* enumeration.
- `OK`, `WARNING`, and `ERROR` are the elements of the enumeration, associated with values 0, 1, and 2 respectively.
- `t_status` is an alias for `enum { OK, WARNING, ERROR }`, allowing you to declare variables of type `t_status` to represent different statuses.

</div>

</v-clicks>

</div>

---

# Enumeration values

> - By default, each element is associated with an integer (0, 1, 2, ...)
> - The first element has value 0, the second 1, etc.
> - You can also assign specific values to each element

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

```c
#include <stdio.h>

typedef enum { RED, GREEN, BLUE } t_color;

int main() {
    t_color c;
    printf("Enter a color: ");
    scanf("%d", &c); // Enter 2
    
    if (c == BLUE)
        printf("Blue!");
    else
        printf("Not blue! (Really?)");
    return 0;
}
```

</div>

<div>

```c
#include <stdio.h>

typedef enum e_volume { 
    WEAK = 10, 
    MID = 50, 
    LOUD = 100 
} t_volume;

int main() {
    t_volume v = WEAK;
    // Memory size of v: sizeof(t_volume) = 4
    printf("Memory size of v: %lu\n", sizeof(v)); 
    printf("Value of an element: %d\n", WEAK); // 10
    return 0;
}
```

</div>

</v-clicks>

</div>

---
layout: intro
---

# Structured types

---

## Definition

<v-clicks>

- *A structured type* is a data type that groups several elements (called *members* or *fields*) of different types under a single name.
- It allows you to represent complex entities by grouping different properties in a single data structure.

## Why?

- Group different properties of the same *entity* in a single data structure.
  - Examples: a date (day, month, year), a person (name, age), a student (first name, last name, birth date), etc.
-  You can group heterogeneous data (of different types) in a single structure, making it easier to manage complex data.

</v-clicks>

---

## Syntax

<v-clicks>

- To define a new structure, use the `struct` keyword followed by the structure name and the list of fields in braces:
   
```c
struct s_struct_name {
    type1 field1;
    type2 field2;
    ...
};
```

- Then, you can redefine this structure to create a new structured type:

```c
typedef struct s_struct_name t_struct_name;
```

## Example

```c
struct s_student {
    char* name;
    unsigned int age;
};
typedef struct s_student t_student;
```

</v-clicks>

---

# Alternative syntax

- You can also define and redefine the structure in a single step (using the same principle as for enumerations):

<div grid="~ cols-2 gap-4">
<v-clicks>
<div>

### For an unnamed structure:

*Definition:*
```c
typedef struct {
    type1 field1;
    type2 field2;
    ...
} t_struct_name;
```

*Example:*

```c
typedef struct {
    char* name;
    unsigned int age;
} t_student;
```

</div>
<div>

### For a named structure:

*Definition:*

```c
typedef struct s_struct_name {
    type1 field1;
    type2 field2;
    ...
} t_struct_name;
```

*Example:*

```c
typedef struct s_student {
    char* name;
    unsigned int age;
} t_student;
```

</div>
</v-clicks>
</div>

---

# Using a structure

<v-clicks>

- Once the structure is defined, you can: 
  - Declare variables of this structured type, declare pointers to structures
  - Use them as function parameters, as function return types, as fields of other structures, etc.

- Example:

```c
t_student s1;
t_student* s2;
t_student array_students[10];
```

```c
void print_student(t_student s);
t_student create_student(char* name, unsigned int age);
```

</v-clicks>

---

# Initialization and field access

> - Structure fields can be initialized when declaring the variable or after declaration.
> - Access to structure fields is done using the `.` operator.

<v-clicks>

### Syntax

```c
t_struct_name var = {field1_value, field2_value, ...};
var.field1 = new_value1;
var.field2 = new_value2;
```

### Example

<div grid="~ cols-[1fr_2fr] gap-4">

<div>

```c
typedef struct {
    char* name;
    unsigned int age;
} t_student;
```

</div>

<div>

```c
t_student s1 = {"Alice", 20}; // Initialization at declaration
t_student s2; // Declaration without initialization
s2.name = "Bob"; // Initialization after declaration
s2.age = 22;
printf("Name: %s, Age: %u\n", s1.name, s1.age); // Access to s1 fields
printf("Name: %s, Age: %u\n", s2.name, s2.age); // Access to s2 fields
```
</div>

</div>

</v-clicks>

---

## Pointer to a structure

- A variable of structured type is a variable: it occupies memory space to store the values of its fields.
- You can declare pointers to structures, which allows you to manipulate structures more flexibly, especially for dynamic memory management.

### Accessing fields via a pointer

> - Access to structure fields through a pointer is done using the `->` operator or by dereferencing the pointer and using the `.` operator.
> - We will prefer the use of the `->` operator.

### Example

<div grid="~ cols-[1fr_2fr] gap-4">

<v-clicks>

<div>

```c
typedef struct {
    int day;
    int month;
    int year;
} t_date;
```

</div>
<div>

```c
t_date d1 = {1, 1, 2000};
t_date *d_ptr = &d1;
scanf("%d", &(*d_ptr).day); // access by dot
scanf("%d", &(d_ptr->day)); // access by arrow
printf("Direct access by d1: %d\n", d1.day);
printf("Access by pointer d_ptr: %d\n", d_ptr->day);
```
</div>
</v-clicks>
</div>

---

## Memory representation and usage

- The memory allocated for a structured variable is contiguous: the fields are stored one after the other in memory.
- The order of the fields in the structure determines the order of their storage in memory.

> Fields are *aligned* to optimize memory access, which may add *padding* (filler bytes) between fields to meet processor alignment constraints.

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

```c
typedef struct {
    char name; // 1 byte
    int x;  // 4 bytes
    int y; // 4 bytes
} t_point;
```
```c
t_point p = {'A', 0, 0};
printf("Address of name: %lu\n", &(p.name));
printf("Address of x: %lu\n", &(p.x));
printf("Address of y: %lu\n", &(p.y));
printf("Size of t_point: %lu\n", sizeof(t_point));
```

</div>

<div>

```plaintext
       name             x       y
    ┌───────┬───────┬───────┬──────┐
p   │  'A'  │  ...  │   0   │   0  │
    └───────┴───────┴───────┴──────┘
       @80      |      @84     @88
                v
              padding  
```

> Here, `sizeof(t_point)` may return 12 instead of 9 due to padding added to align `x` and `y` on 4-byte boundaries. 

</div>
</v-clicks>
</div>

---

# Structure composition

> - A structure can contain other structures as fields, allowing you to create more complex and hierarchical data types.
> - To use a structure inside another, simply declare the inner structure before the outer structure.
> - Access to fields is hierarchical: first access the outer structure, then the inner structure, and finally the desired field.

### Example

<div grid="~ cols-[1fr_2fr] gap-4">

<v-clicks>

<div>

```c
#define STR_SIZE 20

typedef struct {
    int day;
    int month;
    int year;
} t_date;

typedef struct {
    char first_name[STR_SIZE];
    char last_name[STR_SIZE];
    t_date birth_date;
} t_student;
```

</div>

<div>

```c
t_student s1 = {"Alice", "Allisson", {1, 1, 2000}};
t_student *s_ptr = &s1;

printf("Name: %s %s\n", s1.first_name, s1.last_name);

printf("Enter birth date (day month year): ");
scanf("%d %d %d", &s1.birth_date.day, &s1.birth_date.month, &s1.birth_date.year);

printf("Birth day: %d\n", s1.birth_date.day);
printf("Birth month: %d\n", s_ptr->birth_date.month);
printf("Birth year: %d\n", (*s_ptr).birth_date.year);
```
</div>
</v-clicks>
</div>

---

# Arrays of structures

> - You can declare arrays of structures, allowing you to store and manipulate multiple instances of the same structure.
> - Access to the fields of a structure in an array is done using the `[]` operator to access the structure instance, then the `.` or `->` operator to access the fields of that instance.

### Example

<div grid="~ cols-[1fr_2fr] gap-4">

<v-clicks>

<div>

```c
#define STR_SIZE 20
#define MAX_STUDENTS 10

typedef struct {
    int day;
    int month;
    int year;
} t_date;

typedef struct {
    char first_name[STR_SIZE];
    char last_name[STR_SIZE];
    t_date birth_date;
} t_student;
```

</div>

<div>

```c
t_student* array_students = (t_student*) malloc(MAX_STUDENTS * sizeof(t_student));

for (int i = 0; i < MAX_STUDENTS; i++) {
    printf("Enter the first name of student %d: ", i + 1);
    scanf("%s", array_students[i].first_name);
    printf("Enter the last name of student %d: ", i + 1);
    scanf("%s", array_students[i].last_name);
    printf("Enter the birth date of student %d (day month year): ", i + 1);
    scanf("%d %d %d", &array_students[i].birth_date.day, 
                      &array_students[i].birth_date.month, 
                      &array_students[i].birth_date.year);
}
free(array_students);
array_students = NULL;
```
</div>
</v-clicks>
</div>

---

# Structures as function parameters

> - A structured variable can be passed as a function parameter.
> - Copying a structure is done field by field: the values of each field are copied into the new variable.
> - For large structures, it is often preferable to pass a pointer to the structure rather than the structure itself to avoid copy costs.

<div grid="~ cols-[1fr_2fr] gap-2">

<v-clicks>

<div>

### Example

```c
typedef struct {
  int day;
  int month;
  int year;
} t_date;
```

</div>
<div>

```c
void read_date(t_date* d) {
    printf("Enter a date (day month year): ");
    scanf("%d %d %d", &d->day, &d->month, &d->year);
}

void print_date(t_date d) {
    printf("Date: %02d/%02d/%04d\n", d.day, d.month, d.year);
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

<v-clicks>

**About the `typedef` operator:**

- `typedef` allows you to create new types by *redefining* existing types

**About enumerations:**

- Enumerations make it easier to manage discrete values
- They are defined using the `enum` keyword and can be redefined with `typedef`
- By default, enumeration elements are associated with integers starting from 0, but you can also assign them specific values

**About structures:**
- Structures group heterogeneous data, called *fields*, under a single name
- They are defined using the `struct` keyword and can be redefined with `typedef`
- Access to structure fields is done using the `.` or `->` operator for pointers
- **The field access operator (`.` or `->`) depends on the type of the variable accessing the field, not the type of the field being accessed** 
</v-clicks>
