---
theme: default
background: #e9e9e9
class: cover
highlighter: shiki
lineNumbers: false
drawings:
  persist: false
transition: slide-left
title: Présentation du module
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

# Présentation du module

TI202 - Structure de données et Programmation 1

**Rado Rakotonarivo**

`rado.rakotonarivo@efrei.fr` | Bureau A401

---

# Objectifs du module

<v-clicks>

- Développement des acquis en algorithmique et en programmation (TI101 et TI102)
- Renforcement des compétences en matière de résolution de problèmes algorithmiques
- Introduction à la programmation en langage C
- Compréhensoin solides des bases théoriques en algorithmique pour concevoir, implanter et analyser des algorithmes en langage C
</v-clicks>

---

# Acquis d'apprentissage

- Maîtrise de techniques avancées en C : pointeurs, structures, allocation dynamique, programmation modulaire, etc.
- Mise en oeuvre de bonnes pratiques de programmation: conventions d'écriture, documentation du code, modularité, traces et tests, gestion des erreurs, gestion de la mémoire, etc.
- Prise progressive d'autonomie dans la résolution de problèmes algorithmiques

---

# Organisation du cours

- 7 cours magistraux de 2 heures (14h)
- 13 séances de Travaux dirigés de 2 heures (26h)
- 12 séances de Travaux pratiques de 2 heures (24h)
- 4 séances consacrées au Projet de fin de module (3 * 2h + 3h = 9h)
- Séances de Permanences de 2h (*présence optionnelle mais fortement recommandée*)

> **Note:** Les P1-Plus et P1-BDX fonctionneront en CTD + TP. Même contenu pédagogique, même volume horaire, séquencement quasi-identique.

---

# Contenu pédagogique

1. **Bases du langage C** : éléments de syntaxe, variables, types de données, opérateurs, entrées/sorties, structures de contrôle
2. **Tableaux et chaînes de caractères** : manipulation, parcours, algorithmes de recherche et de tri
3. **Pointeurs et allocation dynamique** : manipulation, utilisation, gestion de la mémoire
4. **Fonctions en C** : déclaration, définition, appel, passage de paramètres, retour de valeurs.
5. **Type structuré** : définition, manipulation, passage en paramètre, allocation dynamique
6. **Listes chaînées** : définition, opération de base, algorithmes associés

---
layout: image
image: "./assets/seq-classique.png"
backgroundSize: 100%
---

## Séquencement P1, P1-Int, P1-BN

---
layout: image
image: "./assets/seq-plus.png"
backgroundSize: 100%
---

## Séquencement P1-Plus, P1-BDX

---

## Équipe enseignante TD (P1, P1-BN)


| Groupe      | Nom et Prénom          | Email                          |
|-------------|------------------------|--------------------------------|
| P1-SC1 | Fabien CALCADO | `fabien.calcado@efrei.fr`
| P1-SC2 |Kamel CHABCHOUB | `camel.chabchoub@efrei.fr`
| P1-SC3 | Michel LANDSCHOOT | `mlandsnet@yahoo.fr`
| P1-SC4 | Halim DJERROUD | `halim.djerroud@efrei.fr`
| P1-SC5 | Halim DJERROUD | `halim.djerroud@efrei.fr`
| P1-SC6 | Imène BEN KERMI | `imene.benkermi@efrei.fr`
| P1-SC7 + BN | Mourad KMIMECH | `mourad.kmimech@efrei.fr`

---

## Équipe enseignante CTD (P1-Plus)

| Groupe      | Nom et Prénom          | Email                          |
|-------------|------------------------|--------------------------------|
| P1-PM | Fabien CALCADO | `fabien.calcado@efrei.fr`
| P1-P | Safwan CHENDEB |  `safwan.chendeb@efrei.fr`

## Équipe enseignante CTD (P1-BDX)
| Groupe      | Nom et Prénom          | Email                          |
|-------------|------------------------|--------------------------------|
| P1-BDX | Alexandre BLANCHÉ | `alexandre.blanche@efrei.fr`

---

## Équipe enseignante TD (P1-Int)

| Groupe      | Nom et Prénom          | Email                          |
|-------------|------------------------|--------------------------------|
| P1-INT1 | Rado RAKOTONARIVO | `rado.rakotonarivo@efrei.fr`
| P1-INT2 | Kais KLAI | `kais.klai@efrei.fr`
| P1-INT3 | Kais KLAI | `kais.klai@efrei.fr`
| P1-INT4 | Amir CHACHOUI | `amir.chachoui@efrei.fr`


---

# Évaluation

Pour les P1, P1-Int, P1-BDX, P1-BN

| Composante               | Poids  | Date          |
|--------------------------|--------|---------------|
| 1 Devoir écrit (2h)      | 50%    | Semaine 22    |
| 3 Controles continus (25min) | 10% x 3    | Semaine 7, 11, 15 |
| 1 Projet de groupe        | 20%    | À déterminer    |

---

# Évaluation

Pour les P1-Plus

| Composante               | Poids  | Date          |
|--------------------------|--------|---------------|
| 1 Devoir écrit (2h)      | 50%    | Semaine 22    |
| 2 Controles écrits (30min - 1h) | 15% x 2    | Semaine 11, 15 |
| 1 Projet de groupe        | 20%    | À déterminer    |

---

# TDs

- Les exercices à faire sur papier (en préparation du DE qui sera un examen papier).
- Les TDs seront surtout consacrés à la reflexion, la conception de solution, et à l'exécution à la main (traces)
- **La partie codage et exécution machine se fera en TP**.
- Vous êtes priés de préparer les TDs en amont afin de gagner du temps pour les corrections.
- Au besoin, on pourra vous demander de fermer les ordinateurs pour les TDs.

---

# TPs

- Les premiers TPs se feront sur la plateforme en ligne : [zyBooks](https://learn.zybooks.com/library).
- Les liens d'inscriptions et les activités de TP seront communiqués sur Moodle avant le début des séances (de TP).
- Les derniers TPs se feront sur un IDE et Git/GitHub.
- Les exercices de TP sont à réaliser individuellement (*Vous pourrez vous entraîder, mais on évaluera une progression personnelle sur les TP*).
- De manière générale, il n'y aura pas de correction à faire en classe pour les TPs. (*Sauf pour des exercices spécifiques*).

---

# Projet

- Un projet de synthèse en fin de module, à réaliser en binôme (**1 seul trinôme autorisé pour les effectifs impairs**).
- La collaboration se fera via un dépôt git (*Un TP de mise en situation et de prise en main est prévu*)

---

# Supports de cours

Les supports seront mis à disposition durant la semaine de cours sur les espaces moodle:

* P1, P1-BN,  : [TI202](https://moodle.myefrei.fr/course/view.php?id=21906)
* P1-BDX : [TI202B](https://moodle.myefrei.fr/course/view.php?id=22098)
* P1-Plus : [TI202P](https://moodle.myefrei.fr/course/view.php?id=14375)
* P1-Int : [TI202I](https://moodle.myefrei.fr/course/view.php?id=22091)

---

# Informations pratiques

- **Pour toute demande de votre part**: priorité aux mails, puis Teams. (*Chargé de TD/TP > Coordinateur > Responsable du département Info | Responsable réussite étudiante*)
- **Veuillez vous référez au règlement intérieur de l'école pour les règles de vie en classe**: retards, étudiants perturbateurs...

#### Personnes à contacter
- __Coordinateur du module__ : Rado Rakotonarivo [`rado.rakotonarivo@efrei.fr`](rado.rakotonarivo@efrei.fr)
- __Responsable du dpt Info__ : Asma Gabis [`asma.gabis@efrei.fr`](asma.gabis@efrei.fr)
- __RRE P1__ : Jeanine Ndour [`jeanine.ndour@efrei.fr`](jeanine.ndour@efrei.fr)