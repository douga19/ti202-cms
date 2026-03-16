---
theme: default
background: #e9e9e9
class: cover
highlighter: shiki
lineNumbers: false
info: |
  ## TI202 - Tutoriel CLion
  Mise en place d'un environnement de développement C avec CLion
transition: slide-left
title: Tutoriel CLion
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

# Tutoriel CLion

TI202 - Structure de données et Programmation 1

**Rado Rakotonarivo**  
*D'après la documentation JetBrains*

---

# Objectif du tutoriel

Ce tutoriel vous guide pour :

<v-clicks>

- Installer CLion et obtenir une licence étudiante
- Configurer l'environnement pour les TP C
- Créer un projet Hello World
- Comprendre la structure d'un projet CLion

</v-clicks>

---
layout: image-right
image: assets/apply-1.png
backgroundSize: contain
---

# Installation de CLion et obtention d'une licence

- Rendez-vous sur [https://www.jetbrains.com/community/education/#students](https://www.jetbrains.com/community/education/#students)
- Cliquez sur "Apply now" et suivez la procédure avec votre adresse mail étudiante
- Activez votre compte JetBrains et téléchargez CLion
- Installez CLion selon votre système d'exploitation
- Activez la licence via [Activation de la licence CLion](https://www.jetbrains.com/help/clion/register.html#activate-license)

---
layout: image-right
image: assets/apply-2.png
backgroundSize: contain
---

# Installation de CLion et obtention d'une licence

- Rendez-vous sur [https://www.jetbrains.com/community/education/#students](https://www.jetbrains.com/community/education/#students)
- Cliquez sur "Apply now" et suivez la procédure avec votre adresse mail étudiante
- Activez votre compte JetBrains et téléchargez CLion
- Installez CLion selon votre système d'exploitation
- Activez la licence via [Activation de la licence CLion](https://www.jetbrains.com/help/clion/register.html#activate-license)

---
layout: image-right
image: assets/apply-3.png
backgroundSize: contain
---

# Installation de CLion et obtention d'une licence

- Rendez-vous sur [https://www.jetbrains.com/community/education/#students](https://www.jetbrains.com/community/education/#students)
- Cliquez sur "Apply now" et suivez la procédure avec votre adresse mail étudiante
- Activez votre compte JetBrains et téléchargez CLion
- Installez CLion selon votre système d'exploitation
- Activez la licence via [Activation de la licence CLion](https://www.jetbrains.com/help/clion/register.html#activate-license)

---

# Configuration de CLion pour les TP

<v-clicks>

- Suivez la documentation officielle selon votre OS :
  - [Windows (Cygwin)](https://www.jetbrains.com/help/clion/quick-tutorial-on-configuring-clion-on-windows.html#Cygwin)
  - [macOS/Linux](https://www.jetbrains.com/help/clion/quick-tutorial-on-configuring-clion-on-macos.html)
- Vérifiez que le compilateur C est bien détecté dans les paramètres de CLion

</v-clicks>

---
layout: image-right
image: assets/hello-world.png
backgroundSize: contain
---

# Créer un projet Hello World

<v-clicks>

1. Ouvrez CLion
2. Menu `File` → `New` → `Project...`
3. Choisissez `C Executable`, nommez le projet, cliquez sur `Create`
4. Modifiez le fichier `main.c` pour afficher un message
5. Cliquez sur `Run` pour compiler et exécuter

</v-clicks>

---
layout: image-right
image: assets/hello-world-2.png
backgroundSize: contain
---

# Créer un projet Hello World

1. Ouvrez CLion
2. Menu `File` → `New` → `Project...`
3. Choisissez `C Executable`, nommez le projet, cliquez sur `Create`
4. Modifiez le fichier `main.c` pour afficher un message
5. Cliquez sur `Run` pour compiler et exécuter

---

# Comprendre la structure d'un projet CLion

Voici un exemple de structure de projet C dans CLion :

```plaintext
MyProject/
├── CMakeLists.txt
├── main.c
├── functions.c
├── functions.h
├── utils/
│   ├── utils.c
│   └── utils.h
└── tests/
    └── test_main.c
```

---

## Example CMakeLists.txt

```cmake
cmake_minimum_required(VERSION 3.10)
project(MyProject C)

# Add subdirectory for utils if needed
# add_subdirectory(utils)

# Main executable
add_executable(main main.c functions.c utils/utils.c)

# Test executable
add_executable(test tests/test_main.c functions.c utils/utils.c)

# Optionally, set include directories
target_include_directories(main PRIVATE ${CMAKE_SOURCE_DIR} utils)
target_include_directories(test PRIVATE ${CMAKE_SOURCE_DIR} utils)
```

---

## Explanation of Each Line

<v-clicks>

- `cmake_minimum_required(VERSION 3.10)`: Specifies the minimum required version of CMake.
- `project(MyProject C)`: Declares the project name and language (C).
- `add_executable(main main.c functions.c utils/utils.c)`: Defines an executable named `main` built from the listed source files.
- `add_executable(test tests/test_main.c functions.c utils/utils.c)`: Defines a second executable for tests.
- `target_include_directories(main PRIVATE ${CMAKE_SOURCE_DIR} utils)`: Adds the project root and `utils` folder to the include path for `main`.
- `target_include_directories(test PRIVATE ${CMAKE_SOURCE_DIR} utils)`: Adds the same include paths for the test target.
- (Optional) `add_subdirectory(utils)`: If `utils` is a separate CMake project, this line would include it as a subproject.

</v-clicks>

<v-clicks>

- Right-click the project folder in CLion and choose "New" > "C File" or "Header File" to add new files.
- Update `CMakeLists.txt` to include new source files in the appropriate `add_executable` command.
- CLion will automatically detect and index new files for code completion and navigation.

</v-clicks>



# Conseils supplémentaires

<v-clicks>

- Utilisez le débogueur intégré pour comprendre le déroulement de vos programmes
- Utilisez la complétion de code et la navigation rapide pour gagner du temps
- Consultez la documentation CLion pour des fonctionnalités avancées

</v-clicks>

---

# Félicitations !

Vous êtes prêt à développer en C avec CLion pour les TP TI202.

---

# Références

- [Documentation officielle CLion](https://www.jetbrains.com/help/clion/)
- [Guide d'installation JetBrains](https://www.jetbrains.com/help/clion/installation-guide.html)
- [Activation de la licence CLion](https://www.jetbrains.com/help/clion/register.html#activate-license)
