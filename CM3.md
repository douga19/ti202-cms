---
theme: default
background: #e9e9e9
class: cover
highlighter: shiki
lineNumbers: false
info: |
  ## TI202 - Structure de données et Programmation 1
  Cours Magistral 3 - Les pointeurs et l'allocation dynamique
drawings:
  persist: false
transition: slide-left
title: CM3 - Les pointeurs et l'allocation dynamique
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


# Les pointeurs et l'allocation dynamique

TI202 - Structure de données et Programmation 1

**Rado Rakotonarivo**  
*Cours d'Asma Gabis*

---

# Plan du cours

<v-clicks>

1. **Les pointeurs**
   - Représentation de la mémoire
   - Déclaration et manipulation des pointeurs
   - Pointeurs de pointeurs

2. **Pointeurs & Tableaux**
   - Relation entre tableaux et pointeurs
   - Tableaux 2D et pointeurs

3. **L'allocation dynamique des tableaux**
   - `malloc()`, `calloc()`, `free()`, `realloc()`
   - Allocation dynamique de tableaux 2D

4. **Application**

</v-clicks>

---
layout: intro
---

# Les pointeurs

---

## Représentation de la mémoire vive

<v-clicks>

- Lorsqu'un programme est exécuté, une partie de la **mémoire vive (RAM)** de l'ordinateur est allouée pour stocker les données utilisées par le programme (variables, instructions, etc.).
- Cette mémoire est organisée en **cases mémoire** (ou octets) identifiées par des **adresses mémoire** uniques.
- La mémoire vive ressemble à un **tableau divisé en cases numérotées séquentiellement**.

```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│  0  │  1  │  2  │  3  │  4  │  5  │ ... │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┘
```

### Caractéristiques

- Les numéros des cases mémoire **commencent à 0**
- La taille de chaque case est **1 octet** (8 bits)
- La taille totale dépend de la machine

</v-clicks>

---

## Stockage d'une variable en mémoire

<v-clicks>

Lorsqu'une variable est déclarée, un **emplacement mémoire** est réservé pour stocker sa valeur.

### Exemple
```c
char c;
c = 'C';
```

<div grid="~ cols-2 gap-4">

<div>

**Représentation en mémoire :**

```
┌─────────┬────────┬─────┐
| Adresse | Valeur | Nom |
|---------|--------|-----|
| ...     | ...    |     |
| @1599   |        |     |
| @1600   | 'C'    |  c  |
| @1601   |        |     |
| ...     | ...    |     |

```

> ⚠️ L'adresse mémoire d'une variable est l'adresse de son **premier octet**

</div>

<div>

### Points importants

- **Adresse mémoire** : @1600 (où est stockée `c`)
- **Valeur** : `'C'` (stockée dans `c`)
- **Nom symbolique** : `c` (pour accéder à la variable)
- Les adresses mémoire sont représentées en **hexadécimal**

> ⚠️ Dans le cadre du cours les adresses seront représentées en **décimal préfixées par `@`**

</div>

</div>

</v-clicks>

---

## La taille des variables

<v-clicks>

Les valeurs des variables n'occupent pas toujours une seule case en mémoire → Cela dépend de leurs **types**.

### Tailles typiques (dépendent de la machine)
- `char` : **1 octet**
- `int` : **4 octets**
- `double` : **8 octets**

### Opérateur `sizeof`

`sizeof` permet d'obtenir le nombre d'octets qu'occupe un type :

```c
#include <stdio.h>

int main() {
    printf("Le type char occupe %lu octets en mémoire.\n", sizeof(char));
    printf("Le type int occupe %lu octets en mémoire.\n", sizeof(int));
    printf("Le type double occupe %lu octets en mémoire.\n", sizeof(double));
    return 0;
}
```

> `%lu` : format pour afficher un entier long non signé

</v-clicks>

---

## La taille des variables : Effet du stockage en mémoire

<div grid="~ cols-3 gap-4">

<v-clicks>

<div>

```c
char c = 'C'; // 1 octet
```

| Adresse | Valeur |
|---------|--------|
| @1599    | ...    |
| **@1600** | **'C'** |
| @1601    | ...    |

</div>

<div>

```c
int x = 3; // 4 octets
```

| Adresse | Valeur |
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
double pi = 3.14; // 8 octets
```

| Adresse | Valeur |
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

## Récupération de l'adresse d'une variable

<v-clicks>

L'opérateur **`&`** (esperluette) permet de donner l'adresse d'une variable.

### Formats d'affichage
- `%u` : entier non signé (adresse en décimal)
- `%p`: pointeur (adresse en hexadécimal)

### Exemple

```c
int main() {
    int var = 5;
    printf("La valeur de la variable var est : %d\n", var);
    printf("L'adresse de la variable var est : %u\n", &var);
    printf("L'adresse de la variable var en hexadecimal est : %p\n", &var);
    return 0;
}
```

### ⚠️ Important
- L'adresse affichée pour une variable dont le type occupe plus d'1 octet est l'adresse de son **premier octet**
- La notation `&var` a déjà été vue dans la syntaxe de la fonction `scanf`

</v-clicks>

---

# Comment avoir l'adresse d'une variable ? (suite)

<v-clicks>

### Rappel avec `scanf`

```c
int main() {
    int var;
    scanf("%d", &var);  // Stocker la valeur saisie au clavier
                        // dans la variable var en utilisant son adresse
    
    printf("La valeur de la variable var est : %d\n", var);
    printf("L'adresse de la variable var en hexadecimal est : %p\n", &var);
    return 0;
}
```

### Explication
`&var` permet à `scanf` de connaître **l'adresse mémoire** où stocker la valeur saisie.

</v-clicks>

---

# Accès à une variable

<v-clicks>

Il existe deux modes d'accession à une variable en mémoire:

### 1. Accès direct
Le mode utilisé jusqu'à présent : l'accès au contenu de la variable se fait via son **nom symbolique**.

```c
int a = 10;
printf("%d", a);  // Accès direct via le nom
```

### 2. Accès indirect
L'accès à une variable se fait au travers d'une **autre variable intermédiaire** contenant son adresse.


</v-clicks>

---

## Accès indirect : Représentation en mémoire

<v-clicks>

L'accès à une variable `a` se fait au travers d'une autre variable intermédiaire `p` en stockant l'adresse de `a` dans la variable `p`.

<div grid="~ cols-2 gap-4">

<div>

| Adresse | Valeur | Variable |
|---------|--------|----------|
| ...     | ...    |          |
| @1000    | **@5424** | **p** |
| @1008    |        |          |
| ...     | ...    |          |
| @5424    | **10** | **a** |
| @5428    |        |          |

</div>

<div>

### Points clés
- **Valeur de `a`** = 10
- **Adresse de `a`** = @5424
- **Valeur de `p`** = @5424 (adresse de `a`)
- **Adresse de `p`** = @1000
- `p` est une variable **spéciale** qui contient une **adresse mémoire** d'une autre variable.

</div>

</div>

</v-clicks>

---

# Qu'est-ce qu'un pointeur ?

<v-clicks>

### Définition
Un pointeur est une **variable** qui est destinée à **contenir l'adresse d'une autre variable**.

### Pourquoi utiliser un pointeur ?

Un pointeur est utilisé pour **accéder à une variable lorsque l'accès direct via son nom symbolique n'est pas possible ou pas souhaitable**.

### Avantages d'un pointeur

- ⚡ **Accès direct à la mémoire** et manipulation de ses adresses → un des principes fondamentaux les plus puissants de la programmation C (et C++)
- 🚀 **Opérations très rapides** : accès direct à la mémoire à partir d'un code source

</v-clicks>

---

## Manipulation des pointeurs : Déclaration

<v-clicks>

Le caractère **`*`** (astérisque) permet de marquer le type pointeur.

### Syntaxe

```c
Type* Nom_pointeur;
```

<div grid="~ cols-2 gap-4">

<div>

### Éléments de la syntaxe
- **Type** : type de la donnée pointée
- **\*** : signifie qu'il s'agit d'un type pointeur
- **Nom_pointeur** : nom symbolique (commence souvent par `p` ou se termine par `ptr`)

</div>

<div>

### Exemples
```c
int main() {
    int x;    // Variable A
    char b;   // Variable B
    int* px = NULL;  // Pointeur sur int
    char *b_ptr = NULL;   // Pointeur sur char
    return 0;
}
```
</div>

</div>

- **`NULL`** valeur spéciale indiquant que le pointeur vers une adresse nulle (adresse invalide).
- Elle sert à initialiser un pointeur avant de lui affecter une adresse valide.
- Comme les pointeurs sont des variables, toutes les règles connues s'appliquent (affectation, initialisation, etc.).


</v-clicks>

---

# Opérateurs de référencement / déréférencement

<v-clicks>

### L'opérateur `&` (référencement)
- Appelé **opérateur de référencement**
- Lorsqu'il est appliqué sur une variable → Il donne son **adresse**

### L'opérateur `*` (déréférencement)
- Appelé **opérateur de déréférencement**
- Appliqué à une variable de type pointeur
- Il donne la **valeur** de la variable pointée par le pointeur (accès indirect à la variable)

> ⚠️ L'opérateur `*` annule l'effet de l'opérateur `&`

</v-clicks>

---

# Exemple complet : Manipulation des pointeurs

```c
#include <stdio.h>

int main() {
    int x;                  // déclaration d'une variable x
    int* px = NULL;       // déclaration d'un pointeur sur une variable de type int
    x = 5;                  // initialisation de la variable x
    
    // Initialisation d'un pointeur : pour pointer la variable x
    px = &x;              // affecter l'adresse de x à px
    
    // Affichage de la valeur de x normalement
    printf("Accès direct : La valeur de x est: %d \n", x);
    
    // Affichage de l'adresse de x normalement
    printf("Accès direct : L'adresse de x est: %p \n", &x);  // utilisation de l'&
    
    // Affichage de la valeur de x via le pointeur
    printf("Accès indirect : La valeur de x est: %d \n", *px);  // utilisation de l'*
    
    // Affichage de l'adresse de x via le pointeur ==> afficher la valeur du pointeur
    printf("Accès direct : La valeur de px est: %p \n", px);
    
    return 0;
}
```

---

# Attention aux confusions ⚠️

<v-clicks>

Soient les deux variables suivantes :
```c
int c, *pc;  // déclaration d'une variable et d'un pointeur sur une même ligne
```

### Erreurs courantes

<div grid="~ cols-2 gap-4">

<div>

#### ❌ FAUX
```c
pc = c;
```

`pc` est un pointeur alors que `c` ne l'est pas.

```c
*pc = &c;
```

`*pc` est une valeur alors que `&c` est une adresse.

</div>

<div>

#### ✅ CORRECT
```c
pc = &c;
```

`pc` est une adresse et `&c` l'est aussi.

```c
*pc = c;
```

`*pc` est la valeur pointée par `pc` et `c` est une valeur de même type.

</div>

</div>

</v-clicks>

---
layout: image-right
image: /assets/pointer.jpg
backgroundSize: contain
---

## Pointeur de pointeur

<v-clicks>

Que se passe-t-il lorsqu'un pointeur pointe un autre pointeur et non pas une variable normale ? → **Double pointeur**

### Déclaration d'un double pointeur
```c
Type** Nom_pointeur;
```

### Représentation en mémoire
```c
int x = 10;
int* px = &x;        // pointeur simple 
int** ppx = &px;     // pointeur de pointeur
```

est représenté en mémoire comme suit :

```
   px              x             ppx
┌───────┬───────┬──────┬───────┬─────┐
│  @80  │  ...  │  10  │  ...  │ @64 │
└───────┴───────┴──────┴───────┴─────┘
   @64            @80            @104
```

</v-clicks>

---

# Pointeur de pointeur : Exemple

```c
int x = 10;
int* px = &x;        // pointeur simple 
int** ppx = &px;     // pointeur de pointeur
```

<v-clicks>

### Accès aux valeurs
- `x` : valeur directe (10)
- `*px` : valeur via pointeur simple (10)
- `**ppx` : valeur via double pointeur (10)
- `px` : adresse de x
- `*ppx` : adresse de x (même que px)
- `ppx` : adresse de px

</v-clicks>

---
layout: intro
---

# Pointeurs & Tableaux

---

# Quelle est la relation entre un tableau et un pointeur ?

<v-clicks>

### Points clés

- Le nom d'un tableau **s'évalue** en l'**adresse mémoire** de son **premier élément**
- Un tableau est donc représenté par un pointeur sur le type de ses éléments

### Accès aux éléments d'un tableau

**Rappel :** Un tableau est stocké en mémoire sur une zone **contiguë** → Les cases sont positionnées les unes après les autres.

```c
int T[] = {12, 78, 2, 65, 90, 1, 11, 45, 81};
```

est représenté en mémoire comme suit :

```
  T[0]   T[1]   T[2]   T[3]   T[4]   T[5]   T[6]   T[7]   T[8]
┌──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┐
│  12  │  78  │  2   │  65  │  90  │  1   │  11  │  45  │  81  │
└──────┴──────┴──────┴──────┴──────┴──────┴──────┴──────┴──────┘
```
</v-clicks>

---

# Représentation d'un tableau par les pointeurs

<v-clicks>

### Avec les adresses

```
  T[0]   T[1]   T[2]   T[3]   T[4]   T[5]   T[6]   T[7]   T[8]
┌──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┐
│  12  │  78  │  2   │  65  │  90  │  1   │  11  │  45  │  81  │
└──────┴──────┴──────┴──────┴──────┴──────┴──────┴──────┴──────┘
  @80    @84    @88    @92    @96    @100   @104   @108   @112
```
### Calcul des adresses

Une case `T[i]` occupe en mémoire le nombre d'octets du type de sa donnée.  
Ici : `sizeof(int) = 4 octets`

- **@80** = adresse du premier octet de la case `T[0]`
- **@84** = @80 + nombre d'octets occupés par `T[0]` ce qui fait `@80 + (1 × sizeof(int))`
- **@96** = @80 + nombre d'octets occupés par `T[0]`, `T[1]`, `T[2]`, `T[3]` ce qui fait `@80 + (4 × sizeof(int))`

### Conclusion
Le nom du tableau + sa taille logique sont suffisants pour accéder à tous les éléments du tableau.

</v-clicks>

---

## Utilisation des pointeurs avec les tableaux

<v-clicks>

Le nom d'un tableau est un pointeur, on peut donc écrire :

```c
int T[10];
```

### Équivalences valides

| Notation avec pointeur | Notation classique | Description |
|------------------------|-------------------|-------------|
| `*(T + i)` | `T[i]` | Accès à l'élément i |
| `T + i` | `&T[i]` | Adresse de l'élément i |
| `scanf("%d", T + i);` | `scanf("%d", &T[i]);` | Saisie de l'élément i |
| `printf("%d", *(T + i));` | `printf("%d", T[i]);` | Affichage de l'élément i |

**Note :** `i` est multiplié implicitement par `sizeof(type des données de T)`

</v-clicks>

---

## Représentation d'un tableau 2D par les pointeurs : En mémoire

<v-clicks>

En mémoire, un tableau 2D est représenté comme étant un **tableau de tableaux**.

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
    Colonnes                                Colonnes
```

</v-clicks>

---

## Accès à une case d'un tableau 2D : Étapes

<v-clicks>

Pour accéder à `M[i][j]` :



```
                                        ① À partir du tableau M, 
                                        se déplacer vers la case i
        M[0]     M[1]     M[2]     ...       M[i]
     ┌────────┬────────┬────────┬────────┬──────────┐
     │  @L0   │  @L1   │  @L2   │  ...   │   @Li    │
     └────────┴────────┴────────┴────────┴──────────┘
        │                                      │   ② Récupérer l'adresse de la ligne i
        ▼                                      ▼                   M[i][j]
    ┌───────┬───────┬───────┐              ┌───────┬───────┬───────┬─────┐
@L0 |  [0]  |  [1]  |  ...  |          @Li |  [0]  |  [1]  |  ...  | [j] |
    └───────┴───────┴───────┘              └───────┴───────┴───────┴─────┘
    Colonnes                                Colonnes
                                        ③ Se déplacer jusqu'à la colonne j
```

</v-clicks>

---

## Représentation d'un tableau 2D par les pointeurs : En programmation C

<v-clicks>

Soit le tableau 2D : `int M[3][2];`

### Équivalences valides

Pour manipuler un tableau 2D avec les pointeurs :

| Notation avec pointeur | Notation classique | Description |
|------------------------|-------------------|-------------|
| `*((*(M+i)) + j)` | `M[i][j]` | Accès à l'élément `[i][j]` |
| `(*(M+i)) + j` | `&M[i][j]` | Adresse de l'élément `[i][j]` |
| `scanf("%d", (*(M+i)) + j);` | `scanf("%d", &M[i][j]);` | Saisie de l'élément `[i][j]` |
| `printf("%d", *((*(M+i)) + j));` | `printf("%d", M[i][j]);` | Affichage de l'élément `[i][j]` |

**Note :** `i` et `j` sont multipliés implicitement par `sizeof(type des données de M)`

</v-clicks>

---
layout: intro
---

# L'allocation dynamique des tableaux

---

# Allocation de l'espace mémoire

<v-clicks>

### Jusqu'à maintenant : Allocation statique

La déclaration d'une variable entraîne automatiquement la réservation de l'espace mémoire nécessaire (**réservation statique**).

- Le nombre d'octets nécessaires est connu au **moment de compilation** (compilation time)
- Le compilateur calcule cette valeur à partir du type de données de la variable

### MAIS...

Souvent, nous devons travailler avec des données dont nous ne pouvons prévoir le nombre et la grandeur lors de l'écriture du programme :

- La taille des données est connue au **moment de l'exécution** (runtime) seulement
- Nous devons éviter le gaspillage qui consiste à réserver l'espace maximal prévisible

</v-clicks>

---

# Gestion de la mémoire : Zones mémoire

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

### Pile (Stack)

- Utilisée pour les variables définies initialisées / non initialisées, variables locales
- ✅ Allocation **automatique** de la mémoire
- ✅ Libération **automatique** de la mémoire
- ✅ Traitement des données lors de la **compilation** du programme
- ✅ Accès **rapide**

</div>

<div>

### Tas (Heap)

- Utilisée pour l'**allocation dynamique** de la mémoire
- ⚠️ Allocation **manuelle** de la mémoire
- ⚠️ Libération **manuelle** de la mémoire
- ✅ Grande **flexibilité** dans la gestion de la mémoire
- ⚠️ Risque d'utilisation non correcte de la mémoire
- ⚠️ Nécessite plus de **responsabilité** de la part du programmeur

</div>

</v-clicks>

</div>

---

# Gestion de la mémoire : Vue d'ensemble

```
┌──────────────────────────────────────┐
│  Arguments de la ligne de commande   │
├──────────────────────────────────────┤
│                                      │
│              Pile ↓                  │  Croissance vers le bas
│                                      │
├──────────────────────────────────────┤
│                                      │
│                                      │
├──────────────────────────────────────┤
│                                      │
│              Tas ↑                   │  Croissance vers le haut
│                                      │
├──────────────────────────────────────┤
│      Données non initialisées        │
├──────────────────────────────────────┤
│       Données initialisées           │
├──────────────────────────────────────┤
│   Texte / Code source du programme   │
└──────────────────────────────────────┘
```

---

# Allocation dynamique : 

<v-clicks>

### Objectif
Arriver à **réserver ou libérer** de l'espace mémoire au fur et à mesure que nous en avons besoin pendant l'**exécution** du programme.

### Solution
**Allocation dynamique de la mémoire**

En C : Avec la fonction `malloc` et l'opérateur `sizeof`

</v-clicks>

---

# Définition : Allocation dynamique

<v-clicks>

L'allocation dynamique de la mémoire permet de gérer "manuellement" la mémoire utilisée par votre programme.

### Fonctions de la bibliothèque `stdlib.h`

| Fonction | Description |
|----------|-------------|
| **`malloc()`** | Alloue un nombre d'octets contigus et retourne l'adresse du premier octet ainsi alloué |
| **`calloc()`** | Alloue l'espace pour un tableau en initialisant ses valeurs à zéro, et retourne l'adresse du premier octet ainsi alloué |
| **`free()`** | Libère l'espace précédemment alloué dynamiquement |
| **`realloc()`** | Change la taille de l'espace précédemment alloué dynamiquement|

</v-clicks>

---

# La fonction `malloc()`

<v-clicks>

### Pour "memory allocation"

La fonction `malloc()` réserve un bloc mémoire d'une taille donnée et retourne un pointeur de type `void *` (type génrérique) qui peut être "casté" en un pointeur du type souhaité.

### Syntaxe

```c
type* ptr = (type*) malloc(taille);
```

<div grid="~ cols-3 gap-4">

<div>

`type` : type de la donnée pointée par `ptr`

</div>

<div>

`(type*)` : pour caster le type du pointeur retourné

</div>

<div>

`taille` : nombre d'octets à réserver

</div>

</div>

### ⚠️ Important
Si l'espace sur votre machine est insuffisant, l'allocation échoue et retourne **`NULL`** (pointeur nul).

</v-clicks>

---

## La fonction `malloc()` : Généralisation pour un tableau

<v-clicks>

### Généralisation pour le cas d'un tableau T de taille N

```c
type* T = (type*) malloc(N * sizeof(type));
```

<div grid="~ cols-4 gap-2">

<div>

`type` : type de la donnée pointée par `ptr`

</div>

<div>

`(type*)` : pour caster le type du pointeur retourné

</div>

<div>

`N` : nombre d'éléments souhaités dans le tableau

</div>

<div>

`sizeof(type)` : nombre d'octets qu'occupe un type en mémoire

</div>

</div>

### Exemple
```c
int* T = (int*) malloc(10 * sizeof(int));
```

Alloue un tableau de 10 entiers (40 octets si `sizeof(int) == 4`)

</v-clicks>

---

## La fonction `malloc()` : Exemple 1

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    // déclaration d'un pointeur vers un int
    int* A = NULL;
    
    // Allocation d'un bloc mémoire de 4 octets
    A = (int*) malloc(4);
    
    printf("Saisir un entier : \n");
    scanf("%d", A);
    
    printf("Valeur saisie = %d \n", *A);

    free(A);
    A = NULL;  // Bonne pratique
    
    return 0;
}
```

---

## La fonction `malloc()` : Exemple 2

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int* T = NULL;
    int taille;

    printf("Saisir le nombre de valeurs : \n");
    scanf("%d", &taille);
    
    T = (int*) malloc(taille * sizeof(int)); // allocation d'un bloc mémoire de taille * 4 octets
    
    for (int i = 0; i < taille; i++) {
        *(T + i) = i + 1;  // initialisation des valeurs
        printf("T[%d] = %d \n", i, *(T + i)); // affichage des valeurs
    }
    
    free(T);
    T = NULL; 
    return 0;
}
```

---

## La fonction `calloc()`

<v-clicks>

### Pour "contiguous allocation"

La différence entre `malloc()` et `calloc()` est que :
- `malloc()` alloue un **seul bloc** mémoire
- `calloc()` alloue des **blocs multiples** tous de même taille et **initialisés à zéro**

### Syntaxe

```c
type* T = (type*) calloc(N, sizeof(type));
```

<div grid="~ cols-4 gap-2">

<div>

`type` : type de la donnée pointée par `T`

</div>

<div>

`(type*)` : pour caster le type du pointeur retourné

</div>

<div>

`N` : nombre d'éléments souhaités dans le tableau

</div>

<div>

`sizeof(type)` : taille du type en octets

</div>

</div>

</v-clicks>

---

## La fonction `calloc()` : Exemple

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int* T = NULL;
    int taille;
    
    printf("Saisir le nombre de valeurs : \n");
    scanf("%d", &taille);
    
    T = (int*) calloc(taille, sizeof(int)); // allocation d'un bloc mémoire de taille * 4 octets
    
    for (int i = 0; i < taille; i++) {
        *(T + i) = i + 1;  // initialisation des valeurs
        printf("T[%d] = %d \n", i, *(T + i)); // affichage des valeurs
    }

    free(T);
    T = NULL;
    
    return 0;
}
```

---

## La fonction `free()`

<v-clicks>

L'espace mémoire alloué par `calloc()` ou `malloc()` **n'est pas automatiquement libéré** → Il est nécessaire d'utiliser la fonction `free()` pour le libérer.

### Syntaxe
```c
free(T);
```

où `T` est un pointeur alloué dynamiquement

### ⚠️ Points importants

- `free()` libère l'espace mais **ne change pas la valeur du pointeur**
- Penser à lui affecter `NULL` après l'appel de `free()`
- **Ne pas** utiliser `free()` pour libérer un tableau statique

### Exemple complet
```c
int* T = (int*) malloc(10 * sizeof(int));
// ... utilisation de T ...
free(T);
T = NULL;  // Bonne pratique
```

</v-clicks>

---

## La fonction `realloc()`

<v-clicks>

Si l'espace préalablement alloué s'avère **insuffisant ou trop grand**, vous pouvez changer sa taille en utilisant `realloc()`.

### Syntaxe
```c
ptr = realloc(ptr, newsize);
```

<div grid="~ cols-3 gap-2">

<div>

`ptr` : pointeur alloué dynamiquement

</div>

<div>

`newsize` : nouvelle taille souhaitée

</div>

<div>

Mise à jour de `ptr` pour pointer sur le bloc dont la taille a été modifiée

</div>

</div>

### ⚠️ Important
S'il n'y a pas assez d'espace à la suite du bloc courant pour l'étendre, un **nouveau bloc** de la taille demandée est alloué, puis l'ancien bloc est copié dans le nouveau **et l'ancien bloc est libéré** → d'où la mise à jour de `ptr`.

</v-clicks>

---

## La fonction `realloc()` : Exemple

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int* ptr = NULL;
    int i, n1 = 10, n2 = 20;
    
    ptr = (int*) malloc(n1 * sizeof(int)); // allocation de n1 cases
    
    printf("Adresse de la mémoire précédemment allouée : %p\n", ptr);
    
    int* tmp = NULL;
    tmp = realloc(ptr, n2 * sizeof(int)); // réallocation avec n2 cases
    if (tmp) {
        ptr = tmp;
        tmp = NULL;
    }
    
    printf("Adresse de la mémoire après réallocation : %p\n", ptr);
    
    free(ptr);
    ptr = NULL;
    
    return 0;
}
```

---

# Allocation dynamique d'un tableau 2D : Étapes

<v-clicks>

```
┌─────────────────────────────────┐
│   Adresse du tableau 2D M       │  ① Allouer d'abord un espace
├─────────────────────────────────┤     de taille nb_lignes
│ Adresse → tableau ligne 0       │
├─────────────────────────────────┤
│ Adresse → tableau ligne 1       │
├─────────────────────────────────┤  ② Pour chaque ligne,
│ Adresse → tableau ligne 2       │     allouer un espace de
├─────────────────────────────────┤     taille nb_colonnes
│           ...                   │
├─────────────────────────────────┤
│ Adresse → tableau ligne i       │─────→  M[i][j] (colonne j)
└─────────────────────────────────┘
```

### Processus en 2 étapes
1. Allouer un tableau de **pointeurs** (une case par ligne)
2. Pour chaque ligne, allouer un tableau de la taille souhaitée

</v-clicks>

---

# Allocation dynamique d'un tableau 2D : Programme C

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int** M = NULL;
    int nb_lig = 3;
    int nb_col = 4;
    
    // Allouer un espace de taille nb_lig
    // Chaque case est de type pointeur
    M = (int**) malloc(nb_lig * sizeof(int*));
    
    // Pour chaque ligne, allouer le nombre de colonnes nécessaire
    // ==> utiliser une boucle
    for (int i = 0; i < nb_lig; i++) {
        M[i] = (int*) malloc(nb_col * sizeof(int));
    }
    
    // ... utilisation de M ...
    
    return 0;
}
```

---

## Application de `free()` sur un tableau 2D

<v-clicks>

Pour libérer un espace alloué dynamiquement pour un tableau 2D, il faut **désallouer les taleaux dans le sens inverse de leur allocation**.

### Étapes

1. D'abord libérer l'espace des **petits tableaux** (représentant les lignes)
2. Puis, libérer l'espace du **tableau principal** contenant leurs adresses
3. Remettre le pointeur à `NULL`

### Code

```c
// Libérer l'espace des petits tableaux
for(int i = 0; i < nb_lig; i++)
    free(M[i]);

// Libérer l'espace du tableau principal
free(M);

// Remettre le pointeur à NULL
M = NULL;
```

</v-clicks>

---
layout: intro
---

# Récapitulatif

---

## Récapitulatif : Pointeurs et allocation dynamique

<v-clicks>

**Pointeurs**
- Un pointeur est une variable qui contient l'adresse d'une autre variable
- Opérateur `&` : permet d'obtenir l'adresse d'une variable
- Opérateur `*` : permet d'accéder à la valeur pointée par un pointeur
- L'opérateur `*` annule l'effet de l'opérateur `&`
- Pointeur de pointeur : un pointeur qui pointe vers un autre pointeur

**Allocation dynamique**
- L'allocation dynamique permet de réserver de la mémoire pendant l'exécution du programme
- Les fonctions principales `malloc()`, `calloc()`, `realloc()` et `free()` sont déclarées dans `stdlib.h`
- Toujours vérifier si l'allocation dynamique a réussi (pointeur non nul)
- Le nombre de `free()` doit correspondre au nombre d'allocations dynamiques effectuées
- Pour un tableau 2D, libérer d'abord les lignes, puis le tableau principal
- Après avoir libéré un pointeur, il est recommandé de le mettre à `NULL`

</v-clicks>