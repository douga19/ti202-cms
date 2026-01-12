---
theme: default
background: #e9e9e9
class: cover
highlighter: shiki
lineNumbers: false
info: |
  ## TI202 - Structure de données et Programmation 1
  Cours Magistral 1 - Fondamentaux
drawings:
  persist: false
transition: slide-left
title: CM1 - Bases du Langage C
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
</style>

# Bases du Langage C

TI202 - Structure de données et Programmation 1

**Rado Rakotonarivo**  
*Cours d'Asma Gabis*

---

# Plan du cours

<v-clicks>

1. **Présentation du langage C**

2. **Variables, Types et Opérateurs**
   - Variables et Types
   - Opérateurs
   - Conversion de types

3. **Entrées / Sorties en C**
   - `printf()` 
   - `scanf()`

4. **Structures de contrôle**
   - Conditionnelles (`if`, `else`, `switch`)
   - Boucles (`while`, `for`, `do-while`)

</v-clicks>

---
layout: intro
---

# Présentation du langage C
---

# Pourquoi le langage C ?

<v-clicks>

- 🎯 **Langage structuré** à usage multiple
- 📝 **Très concis** : seulement 32 mots-clé
- 🔧 **Langage de prédilection** pour les systèmes embarqués
- ✅ **Stable** et éprouvé
- 🔗 **Assembleur de haut niveau** - proche de la machine
- 🌍 **Très portable** - fonctionne partout
- ⚡ **Code efficace** - performances optimales
- 🏗️ **Fondation** pour beaucoup d'applications: 
  - Systèmes d'exploitation (Linux, Windows)
  - Bases de données (MySQL, PostgreSQL)
  - Outils de développement (GCC, Git)
  - Langages modernes (Python, Java, etc.)
</v-clicks>

---

# Historique du C

<div grid="~ cols-2 gap-8">

<v-click>

### Création du C

- **Développé par** : Denis Ritchie
- **Lieu** : Bell Labs
- **Période** : 1972-1973
- **Contexte** : Développement d'utilitaires pour Unix

</v-click>

<v-click>

### Évolution

- C reste un des langages les plus utilisés
- Fondamental pour comprendre la programmation
- Standard ISO C
- Encore dominant en systèmes embarqués

</v-click>

</div>

---

# Jargon du programmeur

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

### 📄 Code source
Le texte du programme que vous écrivez

```c
int main() {
    printf("Hello World");
    return 0;
}
```

</div>

<div>

### 🔨 Compiler (Build)
Transformer le code source en programme exécutable

```bash
gcc mon_programme.c -o mon_programme
```

</div>

<div>

### ⚙️ Exécutable (Run)
Le programme compilé qu'une machine peut exécuter

```bash
./mon_programme
```

</div>

<div>

### 📚 Bibliothèque
Fonctions prédéfinies du langage C

```c
#include <stdio.h>  // stdio = fonctions E/S
#include <stdlib.h> // stdlib = fonctions utiles
```

</div>

</v-clicks>

</div>

---

# Fichiers entête (.h)

<v-clicks>

- Fichiers spéciaux contenant les **déclarations** de fonctions
- Extension : `.h` (header)
- Inclus au **début du code source** avec `#include`

**Exemples courants :**
```c
#include <stdio.h>      // Entrées/sorties standard (printf, scanf)
#include <stdlib.h>     // Fonctions utilitaires
#include <string.h>     // Manipulation de chaînes
#include <math.h>       // Fonctions mathématiques
```

**Utilisation :**
```c
#include <stdio.h>

int main() {
    printf("Affichage à l'écran\n");
    return 0;
}
```

</v-clicks>

---

# Quelques règles du langage C

<v-clicks>

### 📋 Syntaxe obligatoire

- ✅ Toute instruction se **termine par un point-virgule** `;`
- ✅ **C est sensible à la casse** : `int`, `Int`, `INT` sont différents
- ✅ **Tous les mots-clé en C sont minuscules** : `if`, `while`, `return`
- ✅ L'**indentation est importante** pour la lisibilité (ignorée par le compilateur)


### 📝 Caractères spéciaux

- `\n` = saut de ligne
- `\t` = tabulation
- `\\` = barre oblique inverse

</v-clicks>

---

# Processus : Compiler et exécuter

<v-clicks>

```
┌─────────────────┐
│  Code source    │  (mon_programme.c)<────────┐
│  (ce que vous   │                            |
│   écrivez)      │                            | Erreurs de syntaxe
└────────┬────────┘                            |
         │ Compilation ────────────────────────┘
         ▼                                     ^
┌─────────────────┐                            |
│   Exécutable    │  (mon_programme)           |
│   (programme    │                            | Erreurs de sémantique
│   compilé)      │                            |
└────────┬────────┘                            |                    
         │ Exécution ──────────────────────────┘
         ▼
┌─────────────────┐
│     Résultat    │  (Affichage, fichiers, etc.)
└─────────────────┘
```

### Compilateur

- ⚠️ Afin de compiler et exécuter un programme C, vous aurez besoin d'un *compilateur*.
- ✅ Nous utiliserons `gcc` dans le cadre du cours.

</v-clicks>

---

# Structure d'un programme C

<v-clicks>

```c
#include <stdio.h>

int main() {
    // Déclaration des variables
    int x = 10;
    
    // Instructions
    printf("La valeur de x est : %d\n", x);
    
    // Retour de la fonction
    return 0;
}
```

**Points clé :**
- ✅ `#include <stdio.h>` importe les fonctions d'E/S
- ✅ `main()` est la **fonction principale** obligatoire
- ✅ Les accolades `{}` délimitent le **bloc d'instructions**
- ✅ `return 0;` indique la fin du programme avec succès

</v-clicks>

---

# Les commentaires

<v-clicks>

### Commentaire simple (une ligne)
```c
int age; // variable pour stocker l'âge
```

### Commentaire multiple (plusieurs lignes)
```c
/*
Calcul de la somme
L'utilisateur entre deux nombres
On effectue l'addition
*/
int a, b;
int sum;
```

### Utilité des commentaires
- 📝 Expliquer le code
- 🎯 Clarifier les intentions
- 🔄 Rendre le code compréhensible (pour soi et les autres)
- 🚫 Commenter du code pour le désactiver temporairement

</v-clicks>

---
layout: intro
---

# Variables, Types et Opérateurs 

---

# Variables et Types

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

- Une *variable* est un **nom** assoié à un **emplacement mémoire** qui contient une **valeur**.
- Chaque variable possède les caractéristiques suivantes :
  - Un **nom** (identificateur) : pour la référencer
  - Un **type** : définit la nature de la donnée
  - Une **valeur** : le contenu stocké
  - Une **adresse mémoire** : où elle est stockée

```
┌─────────────────────┐
│   nom_variable      │  <-- Étiquette (nom)
│  ┌───────────────┐  │
│  │      5        │  │  <-- Contenu (valeur)
│  └───────────────┘  │
└─────────────────────┘
```

</div>

<div>

- Un *type* définit la **nature** de la donnée stockée (entier, réel, caractère, etc.).
- Une variable d'un type donné peut avoir **plusieurs valeurs** du même type
- Mais **pas plusieurs types** différents
- Chaque type détermine l'**espace mémoire** utilisé
- Chaque type définit les **opérations possibles**

</div>

</v-clicks>

</div>


---

# Types fréquents en C

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

### Types entiers

| Type | Signification |
|------|---------------|
| `char` | Caractère (1 octet) |
| `int` | Entier (4 octets) |
| `long` | Entier long (8 octets) |

**Exemples :**
```c
char c = 'A';
int nombre = 42;
long grand_nombre = 1000000;
```

</div>

<div>

### Types réels

| Type | Signification |
|------|---------------|
| `float` | Réel simple (4 octets) |
| `double` | Réel double précision (8 octets) |

**Exemples :**
```c
float pi = 3.14;
double precision = 3.14159265;
```

</div>

</v-clicks>

</div>

---

# Déclaration et initialisation

<v-clicks>

### Déclarer sans initialiser
```c
int x;          // Déclarée, valeur aléatoire
float y;        // Déclarée, valeur aléatoire
```

### Déclarer et initialiser
```c
int x = 10;                // Valeur définie : 10
float y = 3.14;            // Valeur définie : 3.14
char c = 'A';              // Valeur définie : 'A'
```

### Déclarer plusieurs variables
```c
int a, b, c;               // Trois entiers
int x = 5, y = 10, z = 15; // Trois entiers initialisés
```

### ⚠️ Bonne pratique
Toujours **initialiser vos variables** pour éviter des comportements imprévisibles !

</v-clicks>

---

# Les constantes

<v-clicks>

- Une *constante* est une valeur fixe qui ne change pas pendant l'exécution du programme.
- Il existe deux types de constantes en C :
  
  1. **Constantes littérales** : valeurs directement écrites dans le code
      ```c
       int x = 42;          // 42 est une constante littérale
       char c = 'A';       // 'A' est une constante littérale
       ```
  2. **Constantes définies par l'utilisateur** : valeurs nommées définies avec `#define` ou `const`
     - Exemple avec `#define` :
       ```c
       #define PI 3.14159
       float cercle_area = PI * r * r;
       ```
     - Exemple avec `const` :
       ```c
       const int MAX_SIZE = 100;
       int array[MAX_SIZE];
       ```
#### Convention

Le nom des constantes est souvent écrit en **MAJUSCULES** pour les différencier des variables.

</v-clicks>

---


# Les opérateurs arithmétiques

| Opérateur | Nom | Effet | Exemple | Résultat |
|-----------|-----|-------|---------|----------|
| `+` | Addition | Additionne | `7 + 3` | `10` |
| `-` | Soustraction | Soustrait | `7 - 3` | `4` |
| `*` | Multiplication | Multiplie | `7 * 3` | `21` |
| `/` | Division | Divise | `7 / 3` | `2` (entiers) |
| `%` | Modulo | Reste de division | `7 % 3` | `1` |
| `=` | Affectation | Assigne une valeur | `x = 5` | `5` |

---

# L'affectation : Syntaxe vs Erreurs

<v-clicks>

### ✅ Correct

```c
x = 5;           // Affecte 5 à x
a = b = 3;       // Équivalent à : b = 3; a = b;
x = y + z;       // Affecte la somme à x
```

### ❌ Erreur courante : Confondre = et ==

```c
if (x = 5)       // ❌ MAUVAIS : affecte 5 à x
if (x == 5)      // ✅ BON : compare x à 5
```

### ❌ Impossibilités

```c
5 = x;           // ❌ ERREUR : On ne peut affecter à une constante
a + b = x;       // ❌ ERREUR : On ne peut affecter à une expression
```

</v-clicks>

---

# Opérateurs d'affectation composée

<v-clicks>

| Opérateur | Syntaxe | Équivalent |
|-----------|---------|-----------|
| `+=` | `x += 5` | `x = x + 5` |
| `-=` | `x -= 3` | `x = x - 3` |
| `*=` | `x *= 2` | `x = x * 2` |
| `/=` | `x /= 4` | `x = x / 4` |
| `%=` | `x %= 3` | `x = x % 3` |

### Exemples
```c
int x = 10;
x += 5;    // x vaut 15
x -= 3;    // x vaut 12
x *= 2;    // x vaut 24
x /= 4;    // x vaut 6
```

</v-clicks>

---

# Incrémentation et Décrémentation

<v-clicks>

### Incrémentation (`++`)
```c
int x = 7;
x++;       // x vaut 8
++x;       // x vaut 9
```

### Décrémentation (`--`)
```c
int x = 7;
x--;       // x vaut 6
--x;       // x vaut 5
```

</v-clicks>

---

## Différence : Pré vs Post

<v-clicks>


**Post-incrémentation** `x++` :
- Utilise la valeur **avant** incrémentation
- Puis ajoute 1

**Pré-incrémentation** `++x` :
- Ajoute 1 **d'abord**
- Puis utilise la valeur

```c
int b, x = 3;
b = x++;    // b = 3, puis x = 4
b = ++x;    // x = 4, puis b = 4
```

</v-clicks>

---

# Opérateurs relationnels (Comparaison)

<v-clicks>

| Opérateur | Nom | Effet | Exemple | Résultat |
|-----------|-----|-------|---------|----------|
| == | Égalité (double égal) | Compare deux valeurs | `7 == 3` | `0` (faux) |
| `<` | Inférieur | Strictement inférieur | `7 < 10` | `1` (vrai) |
| `<=` | Inférieur ou égal | Inférieur ou égal | `7 <= 7` | `1` (vrai) |
| `>` | Supérieur | Strictement supérieur | `7 > 3` | `1` (vrai) |
| `>=` | Supérieur ou égal | Supérieur ou égal | `7 >= 10` | `0` (faux) |
| != | Différent (!=) | Vérifier la différence | `7 != 3` | `1` (vrai) |

### ⚠️ Important
- Retourne `1` si vrai, `0` si faux
- **Ne pas confondre** `=` (affectation) et `==` (comparaison) !

</v-clicks>

---

# Opérateurs logiques

<v-clicks>

| Opérateur | Nom | Syntaxe | Effet |
|-----------|-----|---------|-------|
| `&&` | ET logique | `(cond1) && (cond2)` | Vrai si **toutes** les conditions sont vraies |
| `\|\|` | OU logique | `(cond1) \|\| (cond2)` | Vrai si **au moins une** condition est vraie |
| `!` | NON logique | `!(condition)` | Inverse la condition |

### Exemples
```c
int age = 25;
if (age >= 18 && age <= 65)
    printf("Âge de travail\n");

if (age < 18 || age > 65)
    printf("Hors âge de travail\n");

int estMajeur = (age >= 18) ? 1 : 0;
if (!estMajeur)
    printf("Mineur\n");
```

</v-clicks>

---

# Caractères et chaînes de caractères

<v-clicks>

### Caractère seul : guillemets simples
```c
char a = 'A';
char b = 'Z';
char digit = '5';
```

### Chaîne de caractères : guillemets doubles
```c
char nom[] = "Alice";
char cours[] = "Langage C";
char message[] = "Bonjour le monde";
```

### ⚠️ Attention à la différence
```c
char c = 'A';       // ✅ Caractère unique
char s[] = "ABC";   // ✅ Chaîne de caractères
// char x = "A";    // ❌ ERREUR : utiliser '' pas ""
```

</v-clicks>

---

# Conversion de types (Cast)

<v-clicks>

### Conversion implicite
Le compilateur convertit automatiquement les types (peut causer des pertes)

```c
int x;
double y;
x = 8.324;  // x prend 8 (perte de la partie décimale)
y = 4;      // y prend 4.0 (ajout de décimales)
```

### Conversion explicite (Cast)
Forcer le type souhaité entre parenthèses

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

# Type booléen en C : Pas natif !

<v-click>

<div grid="~ cols-2 gap-4">
<div>

### Solution : Utiliser des conventions
```c
// Par convention :
// 0 = Faux (false)
// Toute autre valeur = Vrai (true)

int ko = 0;   // Faux
int ok = 1;      // Vrai
if (ok) {         // Toujours vrai
    printf("C'est vrai\n");
}
```
</div>

<div>

### Solution : Créer un pseudo-type booléen
```c
#define BOOL int
#define TRUE 1
#define FALSE 0

int main() {
    BOOL verif = TRUE;
    if (verif) {
        printf("C'est vrai\n");
    }
    return 0;
}
```
</div>
</div>

</v-click>

<v-click>

### Depuis C99 : `<stdbool.h>` | Ne sera pas utilisé dans ce cours
```c
#include <stdbool.h>
int main() {
    bool verif = true;
    if (verif) {
        printf("C'est vrai\n");
    }
    return 0;
}
```

</v-click>

---
layout: intro
---

# Entrées et Sorties

---

# Entrées/Sorties en C

<v-clicks>

### `printf()` - Affichage en sortie
```c
#include <stdio.h>

// dans un main()
printf("Hello World!\n");
printf("Mon âge est %d ans.\n", 19);
```

### `scanf()` - Lecture depuis l'entrée
```c
#include <stdio.h>

// dans main()
int age;
printf("Quel est votre âge ? ");
scanf("%d", &age);
printf("Vous avez %d ans.\n", age);
```

`stdio.h` = Fichier d'entête pour les fonctionsStandard Input Output (Entrées/Sorties standard)

</v-clicks>

---

# `printf()` : Affichage formaté

<v-clicks>

```c
printf("message avec %d formats %f spéciaux", 42, 3.14);
```

### Syntaxe générale
- Message entre **guillemets doubles**
- `%format` pour insérer une variable
- Variables énumérées **dans l'ordre** après le message
- `\n` pour un saut de ligne (pas automatique)

### Exemples
```c
int age = 25;
float prix = 19.99;
char nom[] = "Alice";

printf("Âge : %d ans\n", age);
printf("Prix : %f€\n", prix);
printf("Nom : %s\n", nom);
printf("%d * %f = %f\n", age, prix, age * prix);
```

</v-clicks>

---

# Formats de `printf()`

<v-clicks>

| Format | Type | Exemple |
|--------|------|---------|
| `%d` | Entier (int) | `printf("%d", 42)` |
| `%ld` | Entier long (long) | `printf("%ld", 1000000)` |
| `%f` | Réel (float) | `printf("%f", 3.14)` |
| `%lf` | Réel double (double) | `printf("%lf", 3.14159)` |
| `%c` | Caractère (char) | `printf("%c", 'A')` |
| `%s` | Chaîne (string) | `printf("%s", "Bonjour")` |
| `%x` | Hexadécimal | `printf("%x", 255)` |
| `%e` | Notation scientifique | `printf("%e", 1000.0)` |

### Spécificateurs de précision
```c
printf("%.2f€\n", 19.9999);  // 19.99€
printf("%5d\n", 42);          // "   42" (5 caractères)
printf("%-5d\n", 42);         // "42   " (aligné à gauche)
```

</v-clicks>

---

# `scanf()` : Lecture de données

<v-clicks>

```c
#include <stdio.h>

int main() {
    int age;
    float prix;
    
    printf("Quel est votre âge ? ");
    scanf("%d", &age);
    
    printf("Quel est le prix ? ");
    scanf("%f", &prix);
    
    printf("Vous avez %d ans et le prix est %.2f€\n", age, prix);
    return 0;
}
```

### Points importants
- L'opérateur `&` donne l'**adresse mémoire** (sauf pour les chaînes)
- Les variables doivent être **précédées de &** (adresse)
- Les chaînes `char[]` n'ont **pas besoin de &**

</v-clicks>

---

# `scanf()` : Exemples

<v-clicks>

```c
// Lire UN SEUL caractère
char nextChar;
scanf("%c", &nextChar);

// Lire UN NOMBRE RÉEL
float radius;
scanf("%f", &radius);

// Lire DEUX ENTIERS (séparés par espace)
int length, width;
scanf("%d %d", &length, &width);

// Lire DEUX ENTIERS (séparés par point-virgule)
int length, width;
scanf("%d;%d", &length, &width);

// Lire UNE CHAÎNE (sans &)
char nom[50];
scanf("%s", nom);  // Pas de & pour les chaînes!
```

## Formats 

- Le formattage des données correspond à celui de `printf()`

</v-clicks>

---
layout: intro
---

# Structures de contrôle

---

# Structures de contrôle

<v-clicks>

Les structures de contrôle permettent de :
- **Faire des choix** selon des conditions
- **Répéter** des blocs d'instructions

### Deux types principaux

**Structures conditionnelles :**
- `if` / `else`
- `switch` / `case`

**Boucles :**
- `for`
- `while`
- `do-while`

</v-clicks>

---

# L'instruction if

<v-clicks>

```c
if (condition) {
    // Actions exécutées si condition est VRAIE
    instruction1;
    instruction2;
}
```

### Syntaxe
- Les parenthèses autour de la condition sont **obligatoires**
- Les accolades délimitent le bloc (recommandé même pour une seule instruction)
- Condition : expression de comparaison ou logique

### Exemple
```c
int age = 25;
if (age >= 18) {
    printf("Vous êtes majeur\n");
}
```

</v-clicks>

---

# L'instruction if-else

<v-clicks>

```c
if (condition) {
    // Actions si condition VRAIE
} else {
    // Actions si condition FAUSSE
}
```

### Exemple
```c
int delta = -5;
if (delta >= 0) {
    printf("Il existe une ou deux solutions\n");
} else {
    printf("Aucune solution réelle\n");
}
```

</v-clicks>

---

# Instructions if imbriquées

<v-clicks>

```c
int mois = 3;

if (mois == 1) {
    printf("Janvier\n");
} else if (mois == 2) {
    printf("Février\n");
} else if (mois == 3) {
    printf("Mars\n");
} else {
    printf("Autre mois\n");
}
```

### ⚠️ Attention
Ce style devient **difficile à lire** avec beaucoup de cas  
→ Utiliser `switch-case` à la place !

</v-clicks>

---

# L'instruction switch-case

<v-clicks>

```c
switch (variable) {
    case valeur1:
        instructions;
        break;
    case valeur2:
        instructions;
        break;
    default:
        instructions pour le cas par défaut;
}
```

### Exemple
```c
int mois = 1;
switch (mois) {
    case 1:
        printf("Janvier\n");
        break;
    case 2:
        printf("Février\n");
        break;
    default:
        printf("Autre mois\n");
}
```

</v-clicks>

---

# Les boucles : Concepts

<v-clicks>

Une boucle exécute un bloc d'instructions **plusieurs fois**

### Trois types de boucles

**for :**
- Quand on **connaît** le nombre de répétitions (d'itérations)
- Classique pour parcourir un intervalle

**while :**
- Quand on **ne connaît pas** le nombre d'itérations
- On a une condition d'arrêt

**do-while :**
- Comme while mais exécute **au moins une fois**

</v-clicks>

---

# La boucle for

<v-clicks>

```c
for (initialisation; condition; incrémentation) {
    actions;
}
```

### Exemple simple
```c
for (int x = 0; x < 10; x++) {
    printf("%d ", x);
}
// Affiche : 0 1 2 3 4 5 6 7 8 9
```

### Décomposition
```c
for (int i = 1; i <= 5; i++) {
    printf("Itération %d\n", i);
}
// i = 1 → affiche → i++ (i = 2)
// i = 2 → affiche → i++ (i = 3)
// ...jusqu'à i = 6 (condition fausse, stop)
```

</v-clicks>

---

# La boucle while


Quand on **ne sait pas à l'avance** combien de fois répéter

```c
initialisation;
while (condition) {
    actions;
    incrémentation;
}
```

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

### Exemple 1 : Comme un `for`
```c
int x = 0;
while (x < 10) {
    printf("%d ", x);
    x++;
}
// Affiche : 0 1 2 3 4 5 6 7 8 9
```

</div>

<div>

### Exemple 2 : Validation d'entrée

```c
int nombre;
printf("Entrez un nombre positif : ");
scanf("%d", &nombre);

while (nombre < 0) {
    printf("Nombre invalide, réessayez : ");
    scanf("%d", &nombre);
}
printf("Vous avez entré %d\n", nombre);
// Continue jusqu'à ce qu'un nombre positif soit entré
```
</div>

</v-clicks>

</div>


---

# La boucle do-while

<v-clicks>

```c
do {
    actions;
    incrémentation;
} while (condition);
```

### Différence majeure avec `while`
- **Exécutée au moins une fois** même si la condition est fausse
- La condition est vérifiée à la **fin** de chaque itération

### Exemple
```c
int x = 0;
do {
    printf("%d ", x);
    x++;
} while (x < 10);
// Même résultat que for et while
```

### Cas d'usage
- Menu interactif où on veut afficher au moins une fois
- Validation d'entrée avec au moins une tentative

</v-clicks>

---

# `break` et `continue`

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

### `break`
- Quitter **immédiatement** une boucle ou le bloc d'un `switch`
- Exécute l'instruction après la boucle

```c
for (int i = 0; i < 10; i++)
{
    if (i == 5)
        break;  // Sort de la boucle
    printf("%d ", i);
}
// Affiche : 0 1 2 3 4
```
</div>

<div>

### `continue`
- Sauter à l'**itération suivante**
- La condition est réévaluée

```c
for (int i = 0; i < 10; i++)
{
    if (i == 5)
        continue;  // Saute à i=6
    printf("%d ", i);
}
// Affiche : 0 1 2 3 4 6 7 8 9
```
</div>

</v-clicks>

</div>

---

# Comparaison for, while, do-while

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

- Nombre d' itérations connu
- Concis
- Classique

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

- Nombre d' itérations inconnu
- Plus flexible
- Condition au début

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

- Au moins une fois
- Moins courant
- Condition à la fin

</div>

</v-clicks>

</div>
