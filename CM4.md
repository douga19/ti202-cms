---
theme: default
background: #e9e9e9
class: cover
highlighter: shiki
lineNumbers: false
info: |
  ## TI202 - Structure de données et Programmation 1
  Cours Magistral 4 - Fonctions et Modules
transition: slide-left
title: CM4 - Fonctions et Modules
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

# Fonctions et Modules

TI202 - Structure de données et Programmation 1

**Rado Rakotonarivo**  
*Cours d'Asma Gabis*

---

# Plan du cours

<v-clicks>

1. **Les fonctions en C**
    - Catégories de fonctions
    - Prototype, corps et appel d'une fonction
    - Portée des variables : locale vs globale
2. **Passage de paramètres**
    - Rappel sur le passage par valeur et par référence
    - Passage de paramètres en C : passage par pointeur
    - Passage d'un tableau en paramètre 
3. **La notion de module**
    - Fichier d'entête (`.h`)
    - Fichier source (`.c`)
    - Structure minimale d'un projet modulaire C
</v-clicks>

---
layout: intro
---

# Les fonctions en C

---

# Catégories de fonctions

<v-clicks>

- **Fonctions prédéfinies** (librairies standard)
- **Fonctions utilisateur** (définies par le programmeur)

</v-clicks>

---

# Fonctions prédéfinies

<v-clicks>

- Appelées "fonctions de librairies"
- Exemples : `printf()`, `scanf()`, `malloc()`, `free()`
- Utilisation : inclure le fichier `.h` correspondant

```c
#include <stdio.h>
#include <stdlib.h>
```
</v-clicks>

---

# Librairies standards utiles

<v-clicks>

- `<stdbool.h>` : booléens (`true`, `false`)
- `<string.h>` : manipulation de chaînes
- `<math.h>` : fonctions mathématiques
- `<stdlib.h>` : utilitaires, aléatoire

</v-clicks>

---

## Exemples de fonctions de librairie


<div grid="~ cols-2 gap-8">

<div>

<v-click>

**Booléens** `<stdbool.h>` :  permet d'utiliser le type `bool` et les constantes `true` et `false` pour représenter des valeurs booléennes.
```c
#include <stdbool.h>
```
```c
bool pair = true;
```

</v-click>

<v-click>

**Chaînes de caractères** `<string.h>` : fournit des fonctions pour manipuler les chaînes de caractères (tableaux de `char` terminés par un caractère nul `'\0'`).
```c
#include <string.h>
```
```c
strlen(mot); // longueur
strcpy(dest, src); // copie
strcat(dest, src); // concaténation
strcmp(s1, s2); // comparaison
```
</v-click>

</div>

<div>

<v-click>

**Mathématiques** `<math.h>` : offre des fonctions mathématiques courantes.
```c
#include <math.h>
```
```c
pow(x, y); // puissance
sqrt(x); // racine carrée
```

</v-click>

<v-click>

**Aléatoire** `<stdlib.h>` : fournit des fonctions pour la génération *pseudo* aléatoire de nombres.
```c
#include <stdlib.h>
```
```c
srand(seed); // initialisation du générateur de nombres aléatoires avec une graine (seed)
rand(); // nombre aléatoire
```
</v-click>

</div>

</div>


---

# Fonctions utilisateur

<v-clicks>

- Définies par le programmeur
- Permettent de structurer le code
- Deux grandes familles :
  - Fonctions **sans sortie** (`void`)
  - Fonctions **avec sortie** (type de retour)

</v-clicks>

---

# Prototype et corps d'une fonction

<v-clicks>

- **Prototype** : déclaration (signature)
  - Syntaxe : 
  ```c
  type nom_fonction(type1 param1, type2 param2, ...);
  ```
  - Exemple : 
  ```c
  int somme(int, int);
  ```   

- **Corps** : définition
  - Syntaxe : 
  ```c
  type nom_fonction(type1 param1, type2 param2, ...) {
      // corps de la fonction
  }
  ``` 
  - Exemple :
  ```c
  int somme(int x, int y) {
    return x + y;
  }
  ```
</v-clicks>

---

# Appel d'une fonction

<v-clicks>

- On passe des **arguments** lors de l'appel
- Les types et l'ordre doivent correspondre au prototype
- Syntaxe : 
  ```c
  nom_fonction(arg1, arg2, ...);
  ```
- Exemple :
  ```c
  int res = somme(3, 5);
  ```

</v-clicks>

---

# Où est-ce que cela se passe dans le code ?

<v-clicks>

- **Déclaration** : avant tout appel de la fonction
- **Définition** : peut être avant ou après `main()`, mais doit être déclarée avant tout appel
- **Appel** : on appelle une fonction dans la définition d'une autre fonction

### Exemple :

<div grid="~ cols-2 gap-8">

<div>

```c
#include <stdio.h>

// Déclaration de la fonction
int somme(int, int);

int main() {
    int res = somme(3, 5); // Appel de la fonction
    printf("%d\n", res);
    return 0;
}

// Définition de la fonction
int somme(int x, int y) {
    return x + y;
}
```
</div>

<div>

```c
#include <stdio.h>

// Déclaration et Définition de la fonction
int somme(int x, int y) {
    return x + y;
}

int main() {
    int res = somme(3, 5); // Appel de la fonction
    printf("%d\n", res);
    return 0;
}
```

> ✅ Il est possible de déclarer et de définir les fonctions dans un autre fichier que là où se trouve `main()`

</div>

</div>

</v-clicks>

---
layout: two-cols-header
---

# Fonctions avec et sans valeur de retour



::left::

<v-click>

### Fonctions avec valeur de retour

- Retourne une valeur via `return`
- Exemple :
  ```c
  int somme(int a, int b) {
      return a + b;
  }
  ```

</v-click>


::right::

<v-click>

### Fonctions sans valeur de retour


- Ont comme type de retour `void`
- Ne retournent aucune valeur
- Exemple :
  ```c
  void affiche_somme(int a, int b) {
     printf("La somme est %d\n", a + b);
  }
  ```

</v-click>

---

# Les 4 types de fonctions

<v-clicks>

| Paramètres | Sortie | Prototype |
|------------|--------|-----------|
| Oui        | Oui    | `type f(type1 param1, ...)` |
| Oui        | Non    | `void f(type1 param1, ...)` |
| Non        | Oui    | `type f()` |
| Non        | Non    | `void f()` |

</v-clicks>

---

## Portée des variables : locale vs globale

La **portée** d'une variable détermine où elle est accessible dans le code : elle est déterminée par *le bloc dans lequel elle est déclarée*.

<v-clicks>

- **Variable locale** : déclarée dans une fonction, accessible uniquement dans cette fonction
- **Variable globale** : déclarée en dehors des fonctions, accessible partout

```c
#include <stdio.h>

int N; // variable globale

int times_N(int x);

int main() {
    int x = 3; // variable locale
    N = 5; // modifie la variable globale
    printf("%d\n", times_N(x)); // affiche 15
    return 0;
}

int times_N(int x) {
    return N * x; // utilise la variable globale
}

```
</v-clicks>

---
layout: intro
---

# Passage de paramètres

---

## Petit rappel sur ce qui a été vu en TI102

<v-clicks>

- *Passage par valeur/copie* : les arguments sont copiés dans les paramètres, les modifications dans la fonction n'affectent pas les variables de la fonction appelante.
- *Passage par référence* : une référence des variables est transmise, permettant de modifier les variables de la fonction appelante.

<div grid="~ cols-2 gap-8">

<div>
La fonction

```
fonction : mauvais_swap (a: entier, b: entier)
variables locales :
    temp : entier
début
    temp ← a
    a ← b
    b ← temp
fin 
```
Avec un appel :
```
x ← 3
y ← 5
mauvais_swap(x, y)
```

ne modifie pas `x` et `y`.

</div>

<div>
La fonction

```
fonction : swap (a: référence entier, 
                    b: référence entier)
variables locales :
    temp : entier
début
    temp ← a
    a ← b
    b ← temp
fin 
```
Avec un appel :

```
x ← 3
y ← 5
swap(&x, &y)
```

modifie `x` et `y`.
</div>

</div>

</v-clicks>

---

## En C

<v-clicks>

- Il n'y a **que le passage par valeur/copie**.  
- Le **passage par référence n'existe pas en C**. Afin de modifier une variable de la fonction appelante, on effectue un *passage par copie d'adresse* en utilisant des pointeurs.

<div grid="~ cols-2 gap-8">

<div>

La fonction

```c
void mauvais_swap(int x, int y) {
    int temp = x;
    x = y;
    y = temp;
}
```

Avec un appel :

```c
int a = 3;
int b = 5;
mauvais_swap(a, b);
```

ne modifie pas `a` et `b`.

</div>

<div>

La fonction

```c
void swap(int* x, int* y) {
    int temp = *x;
    *x = *y;
    *y = temp;
}
```

Avec un appel :

```c
int a = 3;
int b = 5;
swap(&a, &b);
```

modifie `a` et `b`.

</div>

</div>

</v-clicks>

---
layout: two-cols-header
---

## Bien comprendre le passage par copie d'adresse

::left::

<v-clicks>

Reprenons l'exemple du `swap` :

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
    printf("a = %d, b = %d\n", a, b); // affiche a = 5, b = 3
    return 0;
}
```

</v-clicks>

::right::

<v-clicks>

Voici ce qui se passe en mémoire :

```plaintext
① Avant l'appel de swap
a (main)     b (main)
┌───────┐   ┌───────┐
│   3   │   │   5   │
└───────┘   └───────┘
   @80         @84
② Pendant l'appel de swap
x (swap)     y (swap)
┌───────┐   ┌───────┐
│  @80  │   │  @84  │
└───────┘   └───────┘
  @104        @112
③ Après l'exécution de swap
a (main)     b (main)
┌───────┐   ┌───────┐
│   5   │   │   3   │
└───────┘   └───────┘
   @80         @84
```

</v-clicks>

---

# Passage d'un tableau en paramètre

<v-clicks>

- Comme un tableau s'évalue à l'adresse de son premier élément, **on peut passer un tableau à une fonction en utilisant un pointeur.**
- Il est **nécessaire de préciser la taille du tableau ou de passer un paramètre supplémentaire pour indiquer la taille**, car le pointeur ne contient pas cette information.
- Deux syntaxes possibles pour déclarer un paramètre de type tableau :
  - `type f(type1* tab, int size)`
  - `type f(type1 tab[], int size)`
- L'accès aux éléments reste le même : `tab[i]` ou `*(tab + i)`

### Exemple :

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

# La notion de module

---

# Qu'est-ce qu'un module ?

<v-clicks>

- Un module est un couple de fichiers :
  - **Source** (`.c`)
  - **Entête** (`.h`)
- L'utilisation des modules permet de structurer un projet en sous-parties cohérentes
> La *programmation modulaire* est le principe de diviser un programme en modules indépendants et réutilisables afin de:
>  - Améliorer la lisibilité
>  - Faciliter la maintenance
>  - Favoriser la réutilisation du code

</v-clicks>

---
layout: two-cols-header
---

## Fichier entête (.h)

::left::

<v-click>

> Les *fichiers d'entête* sont utilisés pour déclarer les éléments d'un module qui doivent être accessibles depuis d'autres modules.

Un fichier d'entête peut contenir :
  - Déclarations de types
  - Prototypes de fonctions
  - Variables globales
  - Inclusions nécessaires au module

Il est d'usage d'utiliser des **gardes d'inclusion** pour éviter les inclusions multiples : *elles permettent de s'assurer que le contenu du fichier d'entête n'est inclus qu'une seule fois dans un même fichier source.*

</v-click>

::right::

<v-click>

### Exemple de fichier d'entête

```c {1-2,15|4-6|8-9|11-13|all}{lines:true}
#ifndef FUNCTIONS_H 
#define FUNCTIONS_H

// Inclusions nécessaires
#include <stdio.h>
#include <stdlib.h>

// Définitions de constantes
#define MAX_SIZE 100

// Prototypes de fonctions
int* create_array(int size);
void print_array(int* arr, int size);

#endif // FUNCTIONS_H
```

</v-click>

---

# Fichier source (.c)

<v-clicks>

> C'est dans les *fichiers sources* que sont écrites les définitions des fonctions et la logique du programme. 

- Elles doivent **nécessairement inclure le fichier d'entête du module** pour que les prototypes soient connus et que les types soient définis.
- L'inclusion d'un fichier d'entête se fait avec des guillemets `""` pour les *fichiers locaux*, tandis que les fichiers de la *bibliothèque standard* sont inclus avec des chevrons `< >`.
  
### Exemple :

```c
#include "functions.h"

int* create_array(int size) {
    int* arr = (int*)malloc(size * sizeof(int));
    return (arr) ? arr : NULL; // Vérification de l'allocation
}

void print_array(int* arr, int size) {
    for (int i = 0; i < size; i++) 
        printf("%d ", arr[i]);
    printf("\n");
}
```

</v-clicks>

---

# Structure minimale d'un projet modulaire C

<div grid="~ cols-3 gap-4">

<v-clicks>

<div>

**Fichier d'entête** (`functions.h`)

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

**Fichier source** (`functions.c`)

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

**Programme principal** (`main.c`)

```c
#include <stdio.h>
#include <stdlib.h>

#include "functions.h"

int main() {
    int size = 5;
    int* arr = create_array(size);
    if (arr == NULL) {
        printf("Allocation échouée\n");
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

# Récapitulatif

---

## Points clés à retenir

<v-clicks>

- Les fonctions permettent de structurer le code en C afin de le rendre plus lisible et réutilisable
- Les fonctions peuvent avoir des paramètres et une valeur de retour
- La syntaxe de déclaration et d'appel doit être respectée
  ```c
    type fonction(type1 param1, type2 param2, ...); // prototype
    type fonction(type1 param1, type2 param2, ...) { 
        // corps de la fonction
    } // définition
    type result = fonction(arg1, arg2, ...); // appel
  ```

- La portée des variables détermine leur accessibilité (locale vs globale)
- En C, le passage de paramètres se fait par valeur, mais on peut simuler le passage par référence avec des pointeurs
- Les modules facilitent l'organisation des projets C en séparant les déclarations (fichiers d'entête) des définitions (fichiers sources)

</v-clicks>

