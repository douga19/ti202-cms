---
theme: default
background: #e9e9e9
class: cover
highlighter: shiki
lineNumbers: false
info: |
  ## TI202 - Structure de données et Programmation 1
  Cours Magistral 5 - Les types et les structures
transition: slide-left
title: CM5 - Les types et les structures
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

# Les types & les structures

TI202 - Structure de données et Programmation 1

**Rado Rakotonarivo**  
*Cours d'Asma Gabis*

---

# Plan du cours

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

1. **Définition et redéfinition de types**
    - Le mot-clé `typedef`
    - Exemples de redéfinition de types

2. **Les énumérations**
    - Définition et syntaxe
    - Exemple d'utilisation
    - Valeurs d'une énumération

</div>

<div>

3. **Les structures et les types structurés**
    - Définition et syntaxe
    - Initialisation et accès aux champs
    - Pointeur sur une structure
    - Représentation et occupation mémoire
    - Composition de structures
    - Tableaux de structures
    - Structures en paramètres de fonctions

</div>

</v-clicks>

</div>

---
layout: intro
---

# Définition et redéfinition de types

---

# Le mot-clé `typedef`

## Pourquoi ?

- Créer ses propres types à partir des types de base
- Améliorer la lisibilité du code
    - Exemple : Définir un type `bool` à partir de `int` pour représenter des valeurs booléennes
- Permet des modifications mineurs pour la généralisation du code
    - Exemple : Changer le type d'un tableau d'items de `double` à `int` en modifiant une seule ligne

## Comment ?

- Le mot-clé `typedef` permet de créer un *alias* pour un type existant (redéfini un type existant)
- Syntaxe :
   ```c
   typedef type_existant t_nouveau_type;
  ```

> Par convetion, on préfixera le nom d'un type utilisateur par `t_`. Par exemple : `t_entier`, `t_string`, `t_date`, etc.

---

# Exemples de redéfinition de types

La redéfinition du type `int` en `t_entier` et du type `char*` en `t_string` :
```c
typedef int t_entier;
typedef char* t_string;
```

permet d'utiliser ces nouveaux types dans le code de manière plus expressive :
```c
t_entier x = 42;
printf("%d", x);

t_string cours = "programmation";
printf("%s", cours);
```

---

# Exemples de redéfinition de types

L'opérateur `sizeof` peut prendre en compte les nouveaux types :

```c
typedef double t_item;

t_item* tab = (t_item*) malloc (10 * sizeof(t_item)); // Allocation dynamique d'un tableau de 10 doubles
```

En modifiant uniquement la ligne de redéfinition du type `t_item`, on peut changer le type des éléments du tableau sans avoir à modifier le reste du code :

```c
// Changer double par int :
typedef int t_item;

t_item* tab = (t_item*) malloc (10 * sizeof(t_item)); // Allocation dynamique d'un tableau de 10 entiers
```

---

# Où définir les nouveaux types ?

> - Les nouveaux types sont généralement définis dans des fichiers d'en-tête (`.h`)
> - La règle reste la même : avant d'utiliser un nouveau type dans un fichier source (`.c`), il faut l'avoir défini auparavant, soit dans le même fichier source, soit dans un fichier d'en-tête inclus dans ce fichier source

<div grid="~ cols-[1fr_2fr] gap-4">

<v-clicks>

<div>

### Fichier d'en-tête `items.h`

```c
#ifndef ITEMS_H
#define ITEMS_H

#include <stdlib.h>

// Redéfinition du type double en t_item
typedef double t_item;

t_item* new_items_array(int size);
void free_items_array(t_item* items);

#endif // ITEMS_H
```
</div>

<div>

### Fichier source `items.c`

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

# Les types énumérés

---

## Définition

- Un *type énuméré* ou *une énumération* est une liste de valeurs possibles pour une variable
- Afin de faciliter la lecture du code, on peut associer des noms à ces valeurs, par exemple pour représenter les jours de la semaine, les couleurs, les niveaux de priorité, etc.

<v-clicks>

## Syntaxe

<div grid="~ cols-3 gap-4">

<div>

*Option 1 (enumération nommée puis redéfinition)*
```c
enum e_nom_enum { 
    ELEMENT1,
    ELEMENT2, 
    ELEMENT3, 
    ... 
};
typedef enum e_nom_enum t_nom_enum;
```

</div>


<div>

*Option 2 (énumération non nommée directement redéfinie)*
```c
typedef enum { 
    ELEMENT1, 
    ELEMENT2, 
    ELEMENT3, 
    ... 
} t_nom_type_enum;
```

</div>

<div>

*Option 3 (énumération nommée directement redéfinie)*
```c
typedef enum e_nom_enum { 
    ELEMENT1, 
    ELEMENT2, 
    ELEMENT3, 
    ... 
} t_nom_type_enum;
```
</div>

</div>

> Par convention, les noms des énumérations sont préfixés par `e_` et les éléments de l'énumération sont écrits en MAJUSCULES.

</v-clicks>

---

# Exemple

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

- Dans cet exemple, on a utilisé la syntaxe de l'option 2 pour définir une énumération non nommée directement redéfinie en `t_status`.
- `enum { OK, WARNING, ERROR }` est une énumération *non nommée*.
- `OK`, `WARNING` et `ERROR` sont les éléments de l'énumération, associés respectivement aux valeurs 0, 1 et 2.
- `t_status` est un alias de `enum { OK, WARNING, ERROR }`, ce qui permet de déclarer des variables de type `t_status` pour représenter les différents statuts.

</div>

</v-clicks>

</div>

---

# Valeurs d'une énumération

> - Par défaut chaque élément est associé à un entier (0, 1, 2, ...)
> - Le premier élément a la valeur 0, le second 1, etc.
> - On peut aussi assigner des valeurs spécifiques à chaque élément

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

```c
#include <stdio.h>

typedef enum { RED, GREEN, BLUE } t_color;

int main() {
    t_color c;
    printf("Saisir une couleur : ");
    scanf("%d", &c); // Saisie de 2
    
    if (c == BLUE)
        printf("Bleu !");
    else
        printf("Pas bleu ! (Ah bon ?)");
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
    // Taille mémoire de v : sizeof(t_volume) = 4
    printf("Taille mémoire de v : %lu\n", sizeof(v)); 
    printf("Valeur d'un élément : %d\n", WEAK); // 10
    return 0;
}
```

</div>

</v-clicks>

</div>

---
layout: intro
---

# Les types structurés

---

## Définition

<v-clicks>

- *Un type structuré* est un type de données qui regroupe plusieurs éléments (appelés *membres* ou *champs*) de types différents sous un même nom.
- Il permet de représenter des entités complexes en regroupant différentes propriétés dans une même structure de données.

## Pourquoi ?

- Regrouper différentes propriétés d'un même *entité* dans une même structure de données.
  - Exemples : une date (jour, mois, année), une personne (nom, âge), un étudiant (prénom, nom, date de naissance), etc.
-  Il est possible de regrouper des données hétérogènes (de types différents) dans une même structure, ce qui facilite la gestion de données complexes.

</v-clicks>

---

## Syntaxe

<v-clicks>

- Pour définir une nouvelle structure, on utilise le mot-clé `struct` suivi du nom de la structure et de la liste des champs entre accolades :
   
```c
struct s_nom_struct {
    type1 champ1;
    type2 champ2;
    ...
};
```

- Ensuite, on peut redéfinir cette structure pour créer un nouveau type structuré :

```c
typedef struct s_nom_struct t_nom_struct;
```

## Exemple

```c
struct s_student {
    char* name;
    unsigned int age;
};
typedef struct s_student t_student;
```
</v-clicks>

---

# Syntaxe alternative

- On peut également définir et redéfinir la structure en une seule étape (suivant le même principe que pour les énumérations) :

<div grid="~ cols-2 gap-4">
<v-clicks>
<div>

### Pour une structure non nommée :

*Définition :*
```c
typedef struct {
    type1 champ1;
    type2 champ2;
    ...
} t_nom_struct;
```

*Exemple :*

```c
typedef struct {
    char* name;
    unsigned int age;
} t_student;
```

</div>
<div>

### Pour une structure nommée :

*Définition :*

```c
typedef struct s_nom_struct {
    type1 champ1;
    type2 champ2;
    ...
} t_nom_struct;
```

*Exemple :*

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

# Utilisation d'une structure

<v-clicks>

- Une fois la structure définie, on peut: 
  - Déclarer des variables de ce type structuré, déclarer des pointeurs vers des structures
  - Les utiliser comme paramètres de fonctions, comme types de retour de fonctions, comme champs d'autres structures, etc.

- Exemple :

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

# Initialisation et accès aux champs

> - Les champs d'une structure peuvent être initialisés lors de la déclaration de la variable ou après la déclaration.
> - L'accès aux champs d'une structure se fait à l'aide de l'opérateur `.`.

<v-clicks>

### Syntaxe

```c
t_nom_struct var = {valeur_champ1, valeur_champ2, ...};
var.champ1 = nouvelle_valeur1;
var.champ2 = nouvelle_valeur2;
```

### Exemple

<div grid="~ cols-[1fr_2fr] gap-4">

<div>

```c
typedef struct {
    char* nom;
    unsigned int age;
} t_student;
```

</div>

<div>

```c
t_student s1 = {"Alice", 20}; // Initialisation lors de la déclaration
t_student s2; // Déclaration sans initialisation
s2.nom = "Bob"; // Initialisation après la déclaration
s2.age = 22;
printf("Nom : %s, Age : %u\n", s1.nom, s1.age); // Accès aux champs de s1
printf("Nom : %s, Age : %u\n", s2.nom, s2.age); // Accès aux champs de s2
```
</div>

</div>

</v-clicks>


---

## Pointeur sur une structure

- Une variable de type structuré est une variable : elle occupe un espace mémoire pour stocker les valeurs de ses champs.
- Il est possible de déclarer des pointeurs vers des structures, ce qui permet de manipuler des structures de manière plus flexible, notamment pour la gestion dynamique de la mémoire.

### Accès aux champs via un pointeur

> - L'accès aux champs d'une structure à travers un pointeur se fait à l'aide de l'opérateur `->` ou en déréférençant le pointeur et en utilisant l'opérateur `.`.
> - Nous allons préférer l'utilisation de l'opérateur `->`.

### Exemple

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
scanf("%d", &(*d_ptr).day); // accès par le point
scanf("%d", &(d_ptr->day)); // accès par la flèche
printf("Accès direct par d1 : %d\n", d1.day);
printf("Accès par pointeur d_ptr : %d\n", d_ptr->day);
```
</div>
</v-clicks>
</div>

---

## Représentation et occupation mémoire

- La mémoire allouée pour une variable de type structuré est contiguë : les champs sont stockés les uns à la suite des autres dans la mémoire.
- L'ordre des champs dans la structure détermine l'ordre de leur stockage en mémoire.

> Les champs sont *alignés* sur afin d'optimiser les accès mémoire, ce qui peut entraîner l'ajout de *padding* (octets de remplissage) entre les champs pour respecter les contraintes d'alignement du processeur.

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

```c
typedef struct {
    char name; // 1 octet
    int x;  // 4 octets
    int y; // 4 octets
} t_point;
```
```c
t_point p = {'A', 0, 0};
printf("Adresse de name : %lu\n", &(p.name));
printf("Adresse de x : %lu\n", &(p.x));
printf("Adresse de y : %lu\n", &(p.y));
printf("Taille de t_point : %lu\n", sizeof(t_point));
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

> Ici `sizeof(t_point)` peut retourner 12 au lieu de 9 à cause du padding ajouté pour aligner les champs `x` et `y` sur des adresses multiples de 4 octets. 

</div>
</v-clicks>
</div>

---

# Composition de structures

> - Une structure peut contenir d'autres structures comme champs, ce qui permet de créer des types de données plus complexes et hiérarchiques.
> - Afin d'utiliser une structure à l'intérieur d'une autre, il suffit de déclarer la structure interne avant la structure externe.
> - L'accès aux champs se fait de manière hiérarchique : on accède d'abord à la structure externe, puis à la structure interne, et enfin au champ souhaité.

### Exemple

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

printf("Nom : %s %s\n", s1.first_name, s1.last_name);

printf("Entrez la date de naissance (jour mois année) : ");
scanf("%d %d %d", &s1.birth_date.day, &s1.birth_date.month, &s1.birth_date.year);

printf("Jour de naissance : %d\n", s1.birth_date.day);
printf("Mois de naissance : %d\n", s_ptr->birth_date.month);
printf("Année de naissance : %d\n", (*s_ptr).birth_date.year);
```
</div>
</v-clicks>
</div>

---

# Tableaux de structures

> - Il est possible de déclarer des tableaux de structures, ce qui permet de stocker et de manipuler plusieurs instances d'une même structure.
> - L'accès aux champs d'une structure dans un tableau se fait à l'aide de l'opérateur `[]` pour accéder à l'instance de la structure, puis de l'opérateur `.` ou `->` pour accéder aux champs de cette instance.

### Exemple

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
    printf("Entrez le prénom du student %d : ", i + 1);
    scanf("%s", array_students[i].first_name);
    printf("Entrez le nom du student %d : ", i + 1);
    scanf("%s", array_students[i].last_name);
    printf("Entrez la date de naissance du student %d (jour mois année) : ", i + 1);
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

# Structures en paramètres de fonctions

> - Une variable de type structuré peut être passée en paramètre d'une fonction.
> - La copie d'une structure se fait champ par champ : les valeurs de chaque champ sont copiées dans la nouvelle variable.
> - Pour les structures de grande taille, il est souvent préférable de passer un pointeur vers la structure plutôt que la structure elle-même pour éviter les coûts de copie.

<div grid="~ cols-[1fr_2fr] gap-2">

<v-clicks>

<div>

### Exemple

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
    printf("Entrez une date (jour mois année) : ");
    scanf("%d %d %d", &d->day, &d->month, &d->year);
}

void print_date(t_date d) {
    printf("Date : %02d/%02d/%04d\n", d.day, d.month, d.year);
}
```
</div>
</v-clicks>
</div>

---
layout: intro
---

# Récapitulatif

---

<v-clicks>

**Sur l'operateur `typedef`:**

- `typedef` permet de créer de nouveaux types en *redéfinissant* des types existants

**Sur les énumérations:**

- Les énumérations facilitent la gestion de valeurs discrètes 
- Elle sont définies à l'aide du mot-clé `enum` et peuvent être redéfinies avec `typedef`
- Par défaut, les éléments d'une énumération sont associés à des entiers commençant par 0, mais on peut aussi leur assigner des valeurs spécifiques

**Sur les structures:**
- Les structures regroupent des données hétérogènes, appelées *champs*, sous un même nom
- Elles sont définies à l'aide du mot-clé `struct` et peuvent être redéfinies avec `typedef`
- L'accès aux champs d'une structure se fait à l'aide de l'opérateur `.` ou `->` pour les pointeurs
- **L'opérateur d'accès aux champs (`.` ou `->`) dépend du type de la variable qui veut accéder au champ et non du type du champ auquel on souhaite accéder** 
</v-clicks>
