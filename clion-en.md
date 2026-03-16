---
layout: intro
---

# Developing a C Project with CLion

---

## Setting Up CLion and Creating a New Project

<v-clicks>

- **Install CLion**: Download and install CLion from JetBrains' website. Make sure you have a C compiler (like GCC or Clang) installed on your system.
- **Start CLion** and select "New Project".
- **Choose C Executable** as the project type. Set the project name and location.
- CLion will generate a basic project structure with a `main.c` file and a `CMakeLists.txt` file.

</v-clicks>

---

## Understanding the Project Structure

<v-clicks>

- The main folder contains your project files.
- `main.c`: The default entry point of your program.
- `CMakeLists.txt`: The build configuration file for your project.
- You can add more source files (`.c`) and header files (`.h`) as your project grows.

</v-clicks>

---

## The Role of CMakeLists.txt

<v-clicks>

- `CMakeLists.txt` tells CLion (and CMake) how to build your project.
- It specifies the minimum CMake version, project name, and which source files to compile.
- Example:
  ```cmake
  cmake_minimum_required(VERSION 3.10)
  project(MyProject C)
  add_executable(MyProject main.c functions.c)
  ```
- To add more source files, list them in the `add_executable` command.

</v-clicks>

---

## Creating Individual Binaries

<v-clicks>

- You can create multiple executables in one project by adding more `add_executable` lines in `CMakeLists.txt`:
  ```cmake
  add_executable(main main.c)
  add_executable(test test.c functions.c)
  ```
- Each target will produce a separate binary.

</v-clicks>

---
layout: intro
---

# Example: CMakeLists.txt and Project Structure

---

## Example Project Tree

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
