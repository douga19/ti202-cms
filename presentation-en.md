---
theme: default
background: #e9e9e9
class: cover
highlighter: shiki
lineNumbers: false
drawings:
  persist: false
transition: slide-left
title: Module Presentation
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

# Module Presentation

TI202 - Data Structures and Programming 1

**Rado Rakotonarivo**

`rado.rakotonarivo@efrei.fr` | Office A401

---

# Module Objectives

<v-clicks>

- Build on algorithmic and programming skills (improve skills aquired during TI101 and TI102)
- Strengthen problem-solving skills in algorithms
- Introduction to programming in C language
- Solid theoretical understanding of algorithms to design, implement, and analyze algorithms in C
</v-clicks>

---

# Learning Outcomes

- Understand and apply advanced techniques in C: pointers, structures, dynamic allocation, modular programming, etc.
- Apply good programming practices: coding conventions, code documentation, modularity, tracing and testing, error handling, memory management, etc.
- Gradual autonomy in solving algorithmic problems

---

# Course Organization

- 7 lectures of 2 hours (14h)
- 13 tutorial sessions of 2 hours (26h)
- 12 lab sessions of 2 hours (24h)
- 4 sessions dedicated to the final project (3 * 2h + 3h = 9h)
- Office hours of 2h (*attendance optional but highly recommended*)

> **Note:** P1-Plus and P1-BDX will operate in CTD + TP. Same course content, same hours, nearly identical sequencing.

---

# Course Content

1. **C language basics**: syntax elements, variables, data types, operators, input/output, control structures
2. **Arrays and strings**: manipulation, traversal, search and sort algorithms
3. **Pointers and dynamic allocation**: manipulation, usage, memory management
4. **Functions in C**: declaration, definition, call, parameter passing, return values
5. **Structured types**: definition, manipulation, parameter passing, dynamic allocation
6. **Linked lists**: definition, basic operations, related algorithms

---
layout: image
image: "./assets/seq-classique.png"
backgroundSize: 100%
---

## Sequencing P1, P1-Int, P1-BN

---
layout: image
image: "./assets/seq-plus.png"
backgroundSize: 100%
---

## Sequencing P1-Plus, P1-BDX

---

## Pedagogical team (P1, P1-BN)

| Group      | Name                  | Email                          |
|------------|-----------------------|--------------------------------|
| P1-SC1 | Fabien CALCADO | `fabien.calcado@efrei.fr`
| P1-SC2 |Kamel CHABCHOUB | `camel.chabchoub@efrei.fr`
| P1-SC3 | Michel LANDSCHOOT | `mlandsnet@yahoo.fr`
| P1-SC4 | Halim DJERROUD | `halim.djerroud@efrei.fr`
| P1-SC5 | Halim DJERROUD | `halim.djerroud@efrei.fr`
| P1-SC6 | Imène BEN KERMI | `imene.benkermi@efrei.fr`
| P1-SC7 + BN | Mourad KMIMECH | `mourad.kmimech@efrei.fr`

---

## CTD Team (P1-Plus)

| Group      | Name                  | Email                          |
|------------|-----------------------|--------------------------------|
| P1-PM | Fabien CALCADO | `fabien.calcado@efrei.fr`
| P1-P | Safwan CHENDEB |  `safwan.chendeb@efrei.fr`

## CTD Team (P1-BDX)
| Group      | Name                  | Email                          |
|------------|-----------------------|--------------------------------|
| P1-BDX | Alexandre BLANCHÉ | `alexandre.blanche@efrei.fr`

---

## Pedagogical team (P1-Int)

| Group      | Name                  | Email                          |
|------------|-----------------------|--------------------------------|
| P1-INT1 | Rado RAKOTONARIVO | `rado.rakotonarivo@efrei.fr`
| P1-INT2 | Kais KLAI | `kais.klai@efrei.fr`
| P1-INT3 | Kais KLAI | `kais.klai@efrei.fr`
| P1-INT4 | Amir CHACHOUI | `amir.chachoui@efrei.fr`

---

# Evaluation modalities

For P1, P1-Int, P1-BDX, P1-BN

| Component               | Weight | Date          |
|-------------------------|--------|--------------|
| 1 Written exam (2h)     | 50%    | Week 22      |
| 3 Continuous assessments (25min) | 10% x 3 | Weeks 7, 11, 15 |
| 1 Group project         | 20%    | To be determined |

---

# Evaluation modalities

For P1-Plus

| Component               | Weight | Date          |
|-------------------------|--------|--------------|
| 1 Written exam (2h)     | 50%    | Week 22      |
| 2 Written tests (30min - 1h) | 15% x 2 | Weeks 11, 15 |
| 1 Group project         | 20%    | To be determined |

---

# Tutorials classes

- Exercises to be done on paper (in preparation for the written exam).
- Tutorials will focus on reflection, solution design, and manual execution (tracing)
- **Coding and machine execution will be done in lab sessions**.
- Please prepare tutorials in advance to save time for corrections.
- If needed, you may be asked to close computers during tutorials.

---

# Lab sessions

- The first practicals will be on the online platform: [zyBooks](https://learn.zybooks.com/library).
- Registration links and practical activities will be communicated on Moodle before the sessions start.
- The last practicals will be on an IDE and Git/GitHub.
- Practical exercises are to be done individually (*You may help each other, but personal progress will be assessed*)
- In general, there will be no in-class correction for practicals. (*Except for specific exercises*)

---

# Project

- A synthesis project at the end of the module, to be done in pairs (**Only one group of three allowed for odd numbers**).
- Collaboration will be via a git repository (*A practical session for setup and onboarding is planned*)

---

# Course Materials

Materials will be made available during the course week on Moodle spaces:

* P1, P1-BN: [TI202](https://moodle.myefrei.fr/course/view.php?id=21906)
* P1-BDX: [TI202B](https://moodle.myefrei.fr/course/view.php?id=22098)
* P1-Plus: [TI202P](https://moodle.myefrei.fr/course/view.php?id=14375)
* P1-Int: [TI202I](https://moodle.myefrei.fr/course/view.php?id=22091)

---

## Practical Information

- **For any request**: priority to email, then Teams. (*Tutorial/Lab instructor > Coordinator > Department Head | RRE*)
- **Please refer to the school's internal regulations for classroom rules**: absence, late arrival, class behavior, etc.

#### Contacts
- __Module Coordinator__: Rado Rakotonarivo [`rado.rakotonarivo@efrei.fr`](mailto:rado.rakotonarivo@efrei.fr)
- __Department Head__: Asma Gabis [`asma.gabis@efrei.fr`](mailto:asma.gabis@efrei.fr)
- __RRE__: Jeanine Ndour [`jeanine.ndour@efrei.fr`](mailto:jeanine.ndour@efrei.fr)