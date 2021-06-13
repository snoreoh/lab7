[![Build Status](https://travis-ci.com/snoreoh/lab7.svg?branch=main)](https://travis-ci.com/snoreoh/lab7)

# Homework. Lab #7

  1. Чтобы настроить Hunter-пакет для solver'a мне необходимо сначала создать в папке проекта папку СМаke и из нее прописать команду ```
$wget https://raw.githubusercontent.com/cpp-pm/gate/master/cmake/HunterGate.cmake -O СМake/HunterGate.cmake```
  2. Таким образом, в папку cmake загружается файл HunterGate.cmake.
  3. Потом изменяем CMakeLists.txt таким образом:
```
include("cmake/HunterGate.cmake")

HunterGate(
    URL "https://github.com/cpp-pm/hunter/archive/v0.23.251.tar.gz"
    SHA1 "5659b15dc0884d4b03dbd95710e6a1fa0fc3258d"
)  
//Позволяет докачать недостающие файлы для корректной работы и проверить их целостность.

hunter_add_package(Boost)
find_package(Boost CONFIG REQUIRED)
//Добавляет в проект необходимые файлы.


target_link_libraries(solver PUBLIC Boost::boost solver_lib formatter_ex)
```
  4. Затем создаём файл .travis.yml:
```
language: cpp
compiler:
- gcc
jobs:
  include:
  - name: "all projects"
script:
    - cmake -H. -B_build
    - cmake --build _build
addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
```
