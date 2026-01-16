---
theme: default
background: #e9e9e9
class: cover
highlighter: shiki
lineNumbers: false
info: |
  ## TI202 - Structure de données et Programmation 1
  Cours Magistral 2 - Tableaux et Chaînes de caractères
drawings:
  persist: false
transition: slide-left
title: CM2 - Tableaux et Chaînes de Caractères
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


# Tableaux et Chaînes de Caractères

TI202 - Structure de données et Programmation 1

**Rado Rakotonarivo**  
*Cours d'Asma Gabis*

---

# Plan du cours

<v-clicks>

1. **Les tableaux 1D**
   - Déclaration et initialisation
   - Manipulation des tableaux

2. **Les algorithmes de tri**
   - Tri à bulles
   - Tri par sélection

3. **La recherche dichotomique**

4. **Les tableaux 2D**
   - Manipulation des matrices

5. **Les chaînes de caractères**
   - Déclaration et manipulation

</v-clicks>

---
layout: intro
---

# Les tableaux 1D

---

# Idée de base : Rappel

<div grid="~ cols-2 gap-4">

<v-clicks>

<div>

### Problème initial
Exemple : 7 variables numériques représentant les notes d'un élève

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

### Solution : Le tableau
Regrouper les informations dans un seul et même contenant appelé **tableau** (Array)

```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│  0  │  1  │  2  │  3  │  4  │  5  │  6  │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│val1 │val2 │val3 │val4 │val5 │val6 │val7 │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┘
```

**Équivalence :**
```c
note1 = val1;  // devient  Notes[0] = val1;
note4 = val4;  // devient  Notes[3] = val4;
```

</div>

</v-clicks>

</div>

<v-click>

### ⚠️ Points importants
- À chaque case est associé un **indice**
- Les indices **commencent toujours à partir de 0**
- Le nombre de cases = taille du tableau
- **Contenu de la case** = valeur
- **Indice** (à partir de 0) = position de la valeur

</v-click>

---

# Taille d'un tableau : Rappel

<v-clicks>

Un tableau est caractérisé par deux tailles différentes :

### 📦 Taille physique
- Nombre de cases **réservées** en mémoire
- Définie à la déclaration du tableau
- Ne peut pas être modifiée

### 📝 Taille logique
- Nombre de cases **remplies** par des valeurs significatives
- Peut être différente de la taille physique
- Évolue pendant l'exécution du programme

### ⚠️ Important
Chaque tableau doit être associé à une **variable supplémentaire** contenant sa taille logique

```c
int tableau[100];  // Taille physique = 100
int n = 10;  // Seulement 10 cases utilisées
```

</v-clicks>

---

# Déclaration d'un tableau en C
<v-clicks>

### Syntaxe générale
```c
Type Nom_tableau[taille_physique];
```

- **Type** : indique le type de données à stocker dans le tableau
- **taille_physique** : DOIT être une valeur/expression constante
### Exemples
```c
int ar[10];            // Tableau pouvant contenir 10 entiers au max
float myArray[3284];   // Tableau pouvant contenir 3284 float au max

// Avec une constante définie
#define TAILLE 10
int values[TAILLE];    // Taille définie par une constante
```

### Déclaration multiple
```c
Type Tab1[taille1], Tab2[taille2], ...;

int b[100], x[27];     // Deux tableaux d'entiers
```

</v-clicks>

---

# Initialisation d'un tableau

<v-clicks>

### Initialisation avec taille implicite
```c
// Crochets vides et valeurs entre accolades
// Taille physique = taille logique = nombre de valeurs
int n[] = {1, 2, 3, 4, 5};
```

### Initialisation avec taille explicite
```c
int m[5] = {1, 2, 3, 4, 5};     // Taille = nombre de valeurs
int k[8] = {1, 2, 3};            // Le reste est initialisé à zéro
int z[5] = {0};                  // Tous les éléments à zéro
```

### ⚠️ Règles importantes
- Si **taille physique > nombre de valeurs** → le reste du tableau est initialisé à zéro
- Si **taille physique < nombre de valeurs** → erreur de syntaxe détectée

</v-clicks>

---

# Accès aux éléments d'un tableau

<v-clicks>

On accède à un élément d'un tableau en utilisant le **nom du tableau** et la **position** de cet élément entre crochets.

### Syntaxe
```c
Nom_tableau[indice_element]
```

### Exemple
```c
#include <stdio.h>

int main() {
    int premiers[] = {2, 3, 5, 7, 11, 13, 17, 19};
    
    // À noter que c'est la 4ème valeur de la liste
    printf("La valeur à l'indice 3 est : %d.\n", premiers[3]);
    // Affiche : 7
    
    // Car la numérotation commence à partir de 0
    printf("La 5ème valeur de cette liste est : %d.\n", premiers[4]);
    // Affiche : 11
    
    return 0;
}
```

</v-clicks>

---

# Remplir un tableau

<v-clicks>

### Deux étapes nécessaires

1. **Déterminer la taille logique** (fixe ou saisie par l'utilisateur) ≤ taille physique
2. **Remplir les éléments** un par un → utiliser une boucle

### Exemple complet
```c
#include <stdio.h>

int main() {
    int ar[20];
    int n = 10;
    
    // Saisir 10 entiers
    printf("Saisir %d entiers: \n", n);
    
    // Boucle pour saisir les valeurs une à une
    for (int i = 0; i < n; i++) {
        scanf("%d", &ar[i]);  // Une case est saisie comme une variable
    }
    
    return 0;
}
```

</v-clicks>

---

# Affichage des éléments d'un tableau

<v-clicks>

Les éléments d'un tableau doivent s'**afficher un par un** (contrairement aux chaînes de caractères).

### Exemple
```c
#include <stdio.h>

int main() {
    int ar[] = {2, 12, 34, 11, 8};
    int n = 5;
    
    // Affichage des éléments d'un tableau
    for (int i = 0; i < n; i++) {
        printf("%d ", ar[i]);  // Séparer les valeurs par des espaces
    }
    printf("\n");
    
    return 0;
}
```

**Résultat :**
```
2 12 34 11 8
```

</v-clicks>

---

# Erreurs à éviter (confusion avec Python)

<v-clicks>

### ❌ Taille physique non constante
```c
int n;
...
int T[n];      // À ne pas faire (même si ça peut passer à la compilation)
int T[2*n];    // À ne pas faire
```

### ❌ Saisie d'un tableau en bloc
```c
int T[10];
scanf("%d", T);  // À ne pas faire, il faut remplir case par case (boucle)
```

### ❌ Affichage d'un tableau en bloc
```c
printf("%d", T);  // À ne pas faire, il faut afficher case par case (boucle)
```

</v-clicks>

---

# Erreurs à éviter (suite)

<v-clicks>

### ❌ Indice négatif et fonction len()
```c
int T[10];
T[-1] = 0;     // À ne pas faire
n = len(T);    // À ne pas faire, on ne peut pas avoir la taille d'un tableau
```

### ❌ Comparaison de deux tableaux
```c
int T1[10], T2[10];
...
if (T1 == T2)  // À ne pas faire
    ...
```

Il faut comparer le contenu **case par case** avec une boucle :
```c
int egaux = 1;  // Hypothèse : tableaux égaux
for (int i = 0; i < taille; i++) {
    if (T1[i] != T2[i]) {
        egaux = 0;  // Différence trouvée
        break;
    }
}
```

</v-clicks>

---
layout: intro
---

# Les algorithmes de tri

---

# Trier un tableau : Définition

<v-clicks>

### Qu'est-ce qu'un algorithme de tri ?

Un algorithme de tri permet d'**organiser les éléments** d'un tableau dans un ordre donné :
- **Croissant** : de la plus petite valeur à la plus grande
- **Décroissant** : de la plus grande valeur à la plus petite

### Objectif principal
Faciliter la **recherche** dans un tableau

### Pourquoi plusieurs algorithmes ?
- Recherche de l'algorithme le plus **optimal** en nombre d'opérations effectuées
- Comparaisons, permutations, etc.
- Différentes stratégies selon les cas d'usage

### Exemples d'algorithmes de tri
- Tri à bulles (Bubble Sort)
- Tri par insertion (Insertion Sort)
- Tri par sélection (Selection Sort)
- Et bien d'autres...

</v-clicks>

---

# Tri à bulles : Principe

<v-clicks>

Un des plus simples algorithmes de tri.

### Principe de fonctionnement

1. Parcourir un tableau du début à la fin
2. Comparer les valeurs de deux cases consécutives
3. Si les valeurs ne sont pas dans l'ordre souhaité, les permuter
4. Continuer le processus jusqu'à ce que le tableau soit entièrement trié

### En d'autres termes
- Après une itération de la boucle externe, la **valeur maximum** est positionnée à la fin du tableau
- La boucle interne doit itérée sur les éléments non triés uniquement

</v-clicks>

---
layout: two-cols-header
---

## Implémentation

::left::

### Programme C

```c
#include <stdio.h>
#define TAILLE 100

int main() {
    int A[TAILLE] = {13, 7, 43, 5, 3, 19, 2, 23, 29};
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

### Correspondance des variables

Dans le programme :

- `i` : indice de parcours de la boucle externe (itérations)
- `j` : indice de parcours de la boucle interne (comparaisons)
- `temp` : variable temporaire pour la permutation

### Visualisation

Retrouvez une animation interactive de l'algorithme de tri à bulles sur le site [Visualgo](https://visualgo.net/en/sorting)

---
layout: iframe
url: https://visualgo.net/en/sorting
---

# Tri à bulles : Exemple 

---

# ⚠️ Problème d'efficacité !

<v-click>

L'algorithme continue à tourner et vérifier les valeurs tant qu'il ne les a pas toutes parcourues, **pourtant le tableau est trié à la 6ème itération**.

**Comment l'améliorer ?**

</v-click>

---

# Tri par sélection : Principe

<v-clicks>

Un autre algorithme de tri, souvent plus efficace que le tri à bulles.

### Principe (pour un tri croissant)

1. Rechercher la valeur **minimum** dans le tableau (récupérer sa position)
2. La permuter avec la **première valeur** du tableau → Le minimum occupe sa position finale
3. Considérer la zone non triée et reproduire les deux étapes précédentes

### En d'autres termes
- Diviser le tableau en deux zones : triée et non triée
- À chaque itération, extraire le minimum de la zone non triée et le placer à la fin de la zone triée
- À chaque itération, la taille de la zone triée augmente de 1 et celle de la zone non triée diminue de 1

</v-clicks>

---
layout: two-cols-header
---

## Implémentation

::left::

### Programme C

```c
#include <stdio.h>
#define TAILLE 100

int main() {

    int A[TAILLE] = {13, 7, 43, 5, 3, 19, 2, 23, 29};
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

### Correspondance des variables

Dans le programme :

- `i`: indice de parcours de la zone triée
- `j`: indice de parcours de la zone non triée
- `min`: indice de la valeur minimum trouvée (dans la zone non triée)
- `temp`: variable temporaire pour la permutation

### Visualisation

Retrouvez une animation interactive de l'algorithme de tri par sélection sur le site [Visualgo](https://visualgo.net/en/sorting)

---
layout: iframe
url: https://visualgo.net/en/sorting
---

# Tri par sélection : Exemple

---
layout: intro
---

# La recherche dichotomique

---

# Recherche dichotomique : Principe

<v-clicks>

### Condition préalable
⚠️ Appliquée **uniquement** sur un tableau **trié**

### Principe de l'algorithme
À chaque étape :

1. **Découpage** du tableau `A` en deux sous-tableaux à l'aide d'un indice médian `m`
   - Moitié inférieure
   - Moitié supérieure

2. Utiliser **2 indices** : gauche `l` et droite `r`
   - Calcul de l'indice central `m = (l + r) / 2`
   - Ou bien `m = l + (r - l) / 2` pour éviter les débordements

3. **Comparaison** de la valeur située à l'indice median `m` à la valeur recherchée :
   - Si la valeur recherchée est **égale** à `A[m]`, alors la recherche est terminée
   - Si la valeur recherchée est **supérieure ou égale** à `A[m]`, alors relancer la recherche avec la **moitié supérieure**
   - Sinon relancer la recherche avec la **moitié inférieure**

</v-clicks>

---
layout: two-cols-header
---

::left::

### Programme C

```c
#include <stdio.h>
#define TAILLE 100
int main() {
    int A[TAILLE] = {1, 1, 2, 3, 5, 8, 13, 21, 34, 55};
    int m, n = 10, trouve = 0;
    int valeur = 21; 
    int l = 0;
    int r = n - 1;     
    
    while (l <= r && !trouve) {
        m = (l + r) / 2;       
        if (A[m] == valeur) {
            trouve = 1;         
        } else if (valeur > A[m]) {
            l = m + 1;          
        } else {
            r = m - 1;          
        }
    }
    if (trouve) {
        printf("Valeur trouvée à l'indice %d\n", m);
    } else {
        printf("Valeur non trouvée\n");
    }
    return 0;
}
```

::right::

## Commentaires

Dans le programme :
- `l` : indique le début de la zone de recherche
- `r` : indique la fin de la zone de recherche
- `m` : indice médian
- `trouve` : indicateur de succès de la recherche (1 si trouvée, 0 sinon)
- `l = m + 1` : réduit la zone de recherche à la moitié supérieure
- `r = m - 1` : réduit la zone de recherche à la moitié inférieure

### Visualisation

Retrouvez une animation interactive de la recherche dichotomique sur le ici [Mathwarehouse](https://www.mathwarehouse.com/programming/gifs/binary-vs-linear-search.php)

---
layout: iframe
url: https://www.mathwarehouse.com/programming/gifs/binary-vs-linear-search.php
---

# Recherche dichotomique : Exemple

---

# Recherche dichotomique : Notes

<v-clicks>

### Avantages

- ⚡ **Très rapide** pour les grands tableaux
- 📉 Complexité logarithmique O(log n) 
- 🎯 Beaucoup plus efficace que la recherche séquentielle 

### Inconvénient

- ⚠️ **Nécessite un tableau trié** au préalable

</v-clicks>

---
layout: intro
---

# Les tableaux 2D

---

## Représentation générale : Rappel

<v-clicks>

Un tableau 2D est une structure de données organisée en **lignes** et **colonnes** (matrice).

```
                Colonnes
            j=0   j=1   j=2
           ┌─────┬─────┬─────┐
       i=0 │val1 │val2 │val3 │
           ├─────┼─────┼─────┤
       i=1 │val4 │val5 │val6 │
           ├─────┼─────┼─────┤
Lignes i=2 │val7 │val8 │val9 │
           ├─────┼─────┼─────┤
       i=3 │val10│val11│val12│
           └─────┴─────┴─────┘
```

</v-clicks>

---

# Déclaration d'un tableau 2D

<v-clicks>

### Syntaxe
```c
Type Nom_Mat[TP_lig][TP_col];
```

- **TP_lig** : Nombre de lignes maximum réservées (Taille Physique lignes)
- **TP_col** : Nombre de colonnes maximum réservées (Taille Physique colonnes)

### Exemples
```c
#include <stdio.h>
#define NB_LIG 20
#define NB_COL 10

int main() {
    int M1[100][100];           // Matrice 100x100
    int M2[NB_LIG][NB_COL];     // Matrice 20x10
    
    return 0;
}
```

</v-clicks>

---

# Initialisation d'un tableau 2D

<v-clicks>

### Initialisation en séquence
```c
// Initialisation de la matrice en séquence
int M[3][4] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11};
```

Résultat en mémoire :
```
┌───┬───┬───┬────┐
│ 0 │ 1 │ 2 │  3 │
├───┼───┼───┼────┤
│ 4 │ 5 │ 6 │  7 │
├───┼───┼───┼────┤
│ 8 │ 9 │10 │ 11 │
└───┴───┴───┴────┘
```

### Initialisation par lignes
```c
int M[3][4] = {
    {0, 1, 2, 3},
    {4, 5, 6, 7},
    {8, 9, 10, 11}
};
```

</v-clicks>

---

# Accès à une case d'un tableau 2D

<v-clicks>

Pour accéder à une case, **deux indices** sont nécessaires.

### Syntaxe
```c
Nom_Mat[indice_ligne][indice_colonne]
```

### Exemples
```c
int M1[100][100];
int M2[NB_LIG][NB_COL];

// Saisie de la case d'indices (0, 0)
scanf("%d", &M1[0][0]);

// Affichage de la case d'indices (0, 1)
printf("%d", M2[0][1]);

// Modification d'une valeur
M1[2][3] = 42;
```

</v-clicks>

---

# Remplir un tableau 2D

<v-clicks>

Pour remplir un tableau 2D, on utilise **deux boucles imbriquées** :
- Une boucle pour les **lignes**
- Une boucle pour les **colonnes**

### Exemple complet
```c
#include <stdio.h>
#define NB_LIG 20
#define NB_COL 10

int main() {
    int M1[NB_LIG][NB_COL];
    int i, j, lig = 3, col = 4;
    
    for (i = 0; i < lig; i++) {           // Parcours des lignes
        for (j = 0; j < col; j++) {       // Parcours des colonnes
            printf("Saisir une valeur : ");
            scanf("%d", &M1[i][j]);
        }
    }
    
    return 0;
}
```

</v-clicks>

---

# Affichage d'un tableau 2D

<v-clicks>

Pour afficher un tableau 2D de manière lisible, on utilise **deux boucles imbriquées** avec un saut de ligne après chaque ligne.

### Exemple complet
```c
#include <stdio.h>
#define NB_LIG 20
#define NB_COL 10

int main() {
    // Initialisation de la matrice en séquence
    int M[3][4] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11};
    int i, j, lig = 3, col = 4;
    
    for (i = 0; i < lig; i++) {
        for (j = 0; j < col; j++) {
            // Séparer les valeurs d'une même ligne par 2 tabulations
            printf("%d\t\t", M[i][j]);
        }
        // Saut de ligne avant d'afficher la suivante
        printf("\n");
    }
    
    return 0;
}
```

**Résultat :**
```
0       1       2       3
4       5       6       7
8       9       10      11
```

</v-clicks>

---
layout: intro
---

# Les chaînes de caractères

---

# Chaînes de caractères : Définition

<v-clicks>

Une **chaîne de caractères** est définie comme étant un **tableau à 1D de caractères** qui se termine par le caractère `'\0'`.

### Caractère de fin `'\0'`
- Visuellement composé de **deux caractères** (`\` et `0`)
- Mais ne représente qu'**un seul caractère** (caractère nul)
- Marque la **fin de la chaîne**

### Déclaration
```c
char Nom_chaine[taille_physique];
```

### Important
```
Taille tableau = nombre de caractères + 1 ('\0')
```

</v-clicks>

---

# Déclaration et initialisation

<v-clicks>

### Méthode 1 : Tableau de caractères
```c
// Tableau de caractères + '\0' = chaîne de caractères
char greeting[6] = {'H', 'E', 'L', 'L', 'O', '\0'};
```

### Méthode 2 : Affectation directe (recommandée)
```c
// Le compilateur C place automatiquement le caractère '\0'
char salutation[] = "Hello";
```

Les deux méthodes sont équivalentes, mais la deuxième est plus simple et le compilateur ajoute automatiquement `'\0'`.

</v-clicks>

---

# Représentation en mémoire

<v-clicks>

```c
char salutation[] = "Hello";
```

Représentation en mémoire :

```
┌───┬───┬───┬───┬───┬────┐
│'H'│'e'│'l'│'l'│'o'│'\0'│
└───┴───┴───┴───┴───┴────┘
  0   1   2   3   4    5
  ↑
Indice
```

### Points clés
- L'accès à chacun des caractères se fait par **l'indice**
- Les indices commencent à **0**
- Le caractère `'\0'` occupe une case (indice 5)
- La taille physique est de **6** pour stocker "Hello" (5 lettres + 1 pour `'\0'`)

</v-clicks>

---

# Affichage d'une chaîne de caractères

<v-clicks>

Elle s'affiche **en bloc** avec le format `%s` (contrairement aux tableaux).

### Exemples
```c
char greeting[6] = {'H', 'E', 'L', 'L', 'O', '\0'};
char salutation[] = "Hello";

printf("%s", salutation);  // Affiche : Hello
printf("%s", greeting);    // Affiche : HELLO
```

### Accéder à un caractère individuel

L'accès se fait directement par l'indice avec le format `%c` :

```c
printf("%c", salutation[0]);  // Affiche : H
printf("%c", salutation[1]);  // Affiche : e
printf("%c", salutation[4]);  // Affiche : o
```

</v-clicks>

---

# Saisie d'une chaîne de caractères

<v-clicks>

La saisie se fait **en bloc** avec le format `%s`.

### Syntaxe
```c
char My_str[32];
scanf("%s", My_str);
```

### ⚠️ Important
- **Pas de `&`** pour la saisie d'une chaîne de caractères
- Contrairement aux autres types (`int`, `float`, etc.) qui nécessitent `&`

### Exemple complet
```c
#include <stdio.h>

int main() {
    char nom[50];
    printf("Entrez votre nom : ");
    scanf("%s", nom);  // Pas de &
    printf("Bonjour %s !\n", nom);
    return 0;
}
```

</v-clicks>

---

# Saisie d'une phrase : ❌ `scanf()`

<v-clicks>

### Définition
Une phrase = une suite de mots séparés par des **espaces**

### Problème avec `scanf`

```c
#include <stdio.h>
#define LEN 100

int main() {
    char str[LEN];
    printf("Saisir une chaine de caractères : \n");
    scanf("%s", str);
    printf("%s \n", str);
    return 0;
}
```

**Entrée utilisateur :** `Bonjour tout le monde`

**Résultat :** `Bonjour`

❌ La chaîne `str` est incomplète : `scanf` s'arrête au **premier espace rencontré** !

</v-clicks>

---
layout: two-cols-header
---

## Solution : Utilisation de `fgets`

::left::

<v-clicks>

### Description

- `fgets` permet de lire une ligne complète de l'entrée standard (`stdin`), y compris les espaces et stocke les caractères lus dans une chaîne de caractères.
- Cette fonction lit jusqu'au retour à la ligne `'\n'` ou jusqu'à la taille maximale spécifiée.

### Syntaxe

```c
fgets(nom_chaine, taille_max, stdin);
// stdin : entrée standard (clavier)
// stdin est une variable prédéfinie dans <stdio.h>
```

</v-clicks>


::right::

<v-clicks>

### Exemple complet

```c
#include <stdio.h>
#define LEN 100

int main() {
    char str[LEN];
    printf("Saisir une chaine de caractères : \n");
    fgets(str, LEN, stdin);  // Lire une ligne complète
    printf("%s", str);
    return 0;
}
```

**Entrée utilisateur :** `Bonjour tout le monde`

**Résultat :** `Bonjour tout le monde`

</v-clicks>


---

## Tableaux VS Chaînes de caractères

| Caractéristique | Tableau | Chaîne de caractères |
|----------------|---------|---------------------|
| **Affichage** | Case par case → boucle | En bloc avec `%s` |
| **Saisie** | Case par case → boucle | En bloc avec `%s` |
| **Scanf** | Formats `%d`, `%f`, `%c`... nécessitant `&` | Format `%s` **sans** `&` |
| **Condition d'arrêt** | Taille logique | Le caractère `'\0'` |
| **Accès aux éléments** | Par indice `T[i]` | Par indice `str[i]` |

---

## Exemple comparatif

```c
// Tableau d'entiers
int tab[10];
for (int i = 0; i < 10; i++) scanf("%d", &tab[i]);  // Avec &
for (int i = 0; i < 10; i++) printf("%d ", tab[i]);  // Case par case

// Chaîne de caractères
char str[50];
scanf("%s", str);      // Sans &
printf("%s", str);     // En bloc
```
