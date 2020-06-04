[![Build Status](https://travis-ci.com/STaRiCHDED/Lab04.svg?branch=master)](https://travis-ci.com/STaRiCHDED/Lab04)
## Laboratory work IV
## Tutorial
```sh
$ export GITHUB_USERNAME=STaRiCHDED
$ export GITHUB_TOKEN=*************************************
$ cd ${GITHUB_USERNAME}/workspace
$  pushd .
~/STaRiCHDED/workspace ~/STaRiCHDED/workspace
$ source scripts/activate
$ git clone https://github.com/${GITHUB_USERNAME}/Lab03 projects/Lab04
Клонирование в «projects/Lab04»…
$ cd projects/Lab04
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/Lab04
$ cat > .travis.yml <<EOF
> language: cpp
> EOF
$ cat >> .travis.yml <<EOF
> 
> script:
> - cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
> - cmake --build _build
> - cmake --build _build --target install
> EOF
$ cat >> .travis.yml <<EOF
> 
> addons:
>   apt:
>     sources:
>       - george-edison55-precise-backports
>     packages:
>       - cmake
>       - cmake-data
> EOF
$ travis login --github-token ${GITHUB_TOKEN}
Successfully logged in as STaRiCHDED!
$ travis lint
Hooray, .travis.yml looks valid :)
$ ex -sc '1i|[![Build Status](https://travis-ci.com/STaRiCHDED/Lab04.svg?branch=master)](https://travis-ci.com/STaRiCHDED/Lab04)' -cx README.md
$ cat README.md
$ git add .travis.yml
$ git add README.md
$ git commit -m"added CI"
$ git push origin master


$ travis lint # Проверяет.travis.yml на ошибки, предупреждения
$ travis accounts # Отображает всех учетных записей, для которых можно настроить репозиторий
$ travis sync # Запускает новую синхронизацию с GitHub
$ travis repos # Перечисляет репозитории, на которые пользователь имеет определенные разрешения.
$ travis enable # Активирует проект на TravisCI
$ travis whatsup # Перечисляет самые последние изменения
$ travis branches # Показывает последнюю информацию для каждой ветки
$ travis history # Выводит историю сборки проектов
$ travis show # Отображает общую информацию о последней сборке
```
### Laboratory work III

<a href="https://yandex.ru/efir/?stream_id=vjKAlxJ0UQrs"><img src="https://raw.githubusercontent.com/tp-labs/lab03/master/preview.png" width="640"/></a>

Данная лабораторная работа посвещена изучению систем автоматизации сборки проекта на примере **CMake**

```sh
$ open https://cmake.org/
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab03** на сервисе **GitHub**
- [x] 2. Ознакомиться со ссылками учебного материала
- [x] 3. Выполнить инструкцию учебного материала
- [x] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_USERNAME=STaRiCHDED
```

```sh
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
$ source scripts/activate
```

```sh
$ git clone https://github.com/${GITHUB_USERNAME}/Lab02.git projects/Lab03
Клонирование в «projects/Lab03»…
remote: Enumerating objects: 114, done.
remote: Counting objects: 100% (114/114), done.
remote: Compressing objects: 100% (80/80), done.
remote: Total 114 (delta 37), reused 100 (delta 30), pack-reused 0
Получение объектов: 100% (114/114), 1.28 MiB | 2.09 MiB/s, готово.
Определение изменений: 100% (37/37), готово.
$ cd projects/Lab03
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/Lab03.git
```

```sh
$ g++ -std=c++11 -I./include -c sources/print.cpp
$ ls print.o
print.o
$ nm print.o | grep print
0000000000000095 t _GLOBAL__sub_I__Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSo
0000000000000000 T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSo
0000000000000026 T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E
$ ar rvs print.a print.o
ar: создаётся print.a
a - print.o
$ file print.a
print.a: current ar archive
$ g++ -std=c++11 -I./include -c examples/example1.cpp
$ ls example1.o
example1.o
$ g++ example1.o print.a -o example1
$ ./example1 && echo
hello
```

```sh
$ g++ -std=c++11 -I./include -c examples/example2.cpp
$ nm example2.o
                 U __cxa_atexit
                 U __dso_handle
0000000000000000 V DW.ref.__gxx_personality_v0
                 U _GLOBAL_OFFSET_TABLE_
000000000000016f t _GLOBAL__sub_I_main
                 U __gxx_personality_v0
0000000000000000 T main
                 U __stack_chk_fail
                 U _Unwind_Resume
0000000000000126 t _Z41__static_initialization_and_destruction_0ii
                 U _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E
                 U _ZNSaIcEC1Ev
                 U _ZNSaIcED1Ev
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEEC1EPKcSt13_Ios_Openmode
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEED1Ev
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEC1EPKcRKS3_
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEED1Ev
                 U _ZNSt8ios_base4InitC1Ev
                 U _ZNSt8ios_base4InitD1Ev
0000000000000000 r _ZStL19piecewise_construct
0000000000000000 b _ZStL8__ioinit
0000000000000000 W _ZStorSt13_Ios_OpenmodeS_
$ g++ example2.o print.a -o example2
$ ./example2
$ cat log.txt && echo
hello
```

```sh
$ rm -rf example1.o example2.o print.o
$ rm -rf print.a
$ rm -rf example1 example2
$ rm -rf log.txt
```

```sh
$ cat > CMakeLists.txt <<EOF
cmake_minimum_required(VERSION 3.4)
project(print)
EOF
```

```sh
$ cat >> CMakeLists.txt <<EOF
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
EOF
```

```sh
$ cat >> CMakeLists.txt <<EOF
add_library(print STATIC \${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
EOF
```

```sh
$ cat >> CMakeLists.txt <<EOF
include_directories(\${CMAKE_CURRENT_SOURCE_DIR}/include)
EOF
```

```sh
$ cmake -H. -B_build
-- The C compiler identification is GNU 7.5.0
-- The CXX compiler identification is GNU 7.5.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab03/_build

$ cmake --build _build
Scanning dependencies of target print
[ 50%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[100%] Linking CXX static library libprint.a
[100%] Built target print
```

```sh
$ cat >> CMakeLists.txt <<EOF

add_executable(example1 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example1.cpp)
add_executable(example2 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example2.cpp)
EOF
```

```sh
$ cat >> CMakeLists.txt <<EOF

target_link_libraries(example1 print)
target_link_libraries(example2 print)
EOF
```

```sh
$ cmake --build _build
-- Configuring done
-- Generating done
-- Build files have been written to: /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab03/_build
[ 33%] Built target print
Scanning dependencies of target example2
[ 50%] Building CXX object CMakeFiles/example2.dir/examples/example2.cpp.o
[ 66%] Linking CXX executable example2
[ 66%] Built target example2
Scanning dependencies of target example1
[ 83%] Building CXX object CMakeFiles/example1.dir/examples/example1.cpp.o
[100%] Linking CXX executable example1
[100%] Built target example1
$ cmake --build _build --target print
$ cmake --build _build --target example1
$ cmake --build _build --target example2
```

```sh
$ ls -la _build/libprint.a
-rw-r--r-- 1 nikitaklimov nikitaklimov 3134 июн  3 13:49 _build/libprint.a
$ _build/example1 && echo
hello
$ _build/example2
$ cat log.txt && echo
hello
$ rm -rf log.txt
```

```sh
$ git clone https://github.com/tp-labs/lab03 tmp
Клонирование в «tmp»…
remote: Enumerating objects: 15, done.
remote: Counting objects: 100% (15/15), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 88 (delta 7), reused 4 (delta 2), pack-reused 73
Распаковка объектов: 100% (88/88), готово.
$ mv -f tmp/CMakeLists.txt .
$ rm -rf tmp
```

```sh
$ cat CMakeLists.txt
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

option(BUILD_EXAMPLES "Build examples" OFF)

project(print)

add_library(print STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)

target_include_directories(print PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
)

if(BUILD_EXAMPLES)
  file(GLOB EXAMPLE_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/examples/*.cpp")
  foreach(EXAMPLE_SOURCE ${EXAMPLE_SOURCES})
    get_filename_component(EXAMPLE_NAME ${EXAMPLE_SOURCE} NAME_WE)
    add_executable(${EXAMPLE_NAME} ${EXAMPLE_SOURCE})
    target_link_libraries(${EXAMPLE_NAME} print)
    install(TARGETS ${EXAMPLE_NAME}
      RUNTIME DESTINATION bin
    )
  endforeach(EXAMPLE_SOURCE ${EXAMPLE_SOURCES})
endif()

install(TARGETS print
    EXPORT print-config
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)

install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/ DESTINATION include)
install(EXPORT print-config DESTINATION cmake)
$ cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
Configuring done
-- Generating done
-- Build files have been written to: /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab03/_build
$ cmake --build _build --target install
[100%] Built target print
Install the project...
-- Install configuration: ""
-- Installing: /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab03/_install/lib/libprint.a
-- Installing: /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab03/_install/include
-- Installing: /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab03/_install/include/print.hpp
-- Installing: /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab03/_install/cmake/print-config.cmake
-- Installing: /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab03/_install/cmake/print-config-noconfig.cmake
$ tree _install
_install
├── cmake
│   ├── print-config.cmake
│   └── print-config-noconfig.cmake
├── include
│   └── print.hpp
└── lib
    └── libprint.a

3 directories, 4 files
```

```sh
$ git add CMakeLists.txt
$ git commit -m"added CMakeLists.txt"
[master cb1748c] added CMakeLists.txt
 1 file changed, 36 insertions(+)
 create mode 100644 CMakeLists.txt
$ git push origin master
Username for 'https://github.com': STaRiCHDED
Password for 'https://STaRiCHDED@github.com': 
Подсчет объектов: 117, готово.
Delta compression using up to 8 threads.
Сжатие объектов: 100% (76/76), готово.
Запись объектов: 100% (117/117), 1.29 MiB | 1017.00 KiB/s, готово.
Total 117 (delta 38), reused 113 (delta 37)
remote: Resolving deltas: 100% (38/38), done.
To https://github.com/STaRiCHDED/Lab03.git
 * [new branch]      master -> master
```

## Report

```sh
$ popd
$ export LAB_NUMBER=03
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Homework

Представьте, что вы стажер в компании "Formatter Inc.".
### Задание 1
Вам поручили перейти на систему автоматизированной сборки **CMake**.
Исходные файлы находятся в директории [formatter_lib](formatter_lib).
В этой директории находятся файлы для статической библиотеки *formatter*.
Создайте `CMakeList.txt` в директории [formatter_lib](formatter_lib),
с помощью которого можно будет собирать статическую библиотеку *formatter*.

### Задание 2
У компании "Formatter Inc." есть перспективная библиотека,
которая является расширением предыдущей библиотеки. Т.к. вы уже овладели
навыком созданием `CMakeList.txt` для статической библиотеки *formatter*, ваш 
руководитель поручает заняться созданием `CMakeList.txt` для библиотеки 
*formatter_ex*, которая в свою очередь использует библиотеку *formatter*.

### Задание 3
Конечно же ваша компания предоставляет примеры использования своих библиотек.
Чтобы продемонстрировать как работать с библиотекой *formatter_ex*,
вам необходимо создать два `CMakeList.txt` для двух простых приложений:
* *hello_world*, которое использует библиотеку *formatter_ex*;
* *solver*, приложение которое испольует статические библиотеки *formatter_ex* и *solver_lib*.

**Удачной стажировки!**

## Homework
### Part 1
```sh
1.
$ mkdir HOMEWORK03
$ cd HOMEWORK03
$ git clone https://github.com/tp-labs/lab03 tmp
$ cd formatter_lib
$ cat > CMakeLists.txt <<EOF
cmake_minimum_required(VERSION 3.10)
project(formatter)
EOF
$ cat >> CMakeLists.txt <<EOF
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
EOF
$cat >> CMakeLists.txt <<EOF
add_library(formatter STATIC \${CMAKE_CURRENT_SOURCE_DIR}/formatter.cpp)
EOF
$cat >> CMakeLists.txt <<EOF
include_directories(\${CMAKE_CURRENT_SOURCE_DIR})
EOF
$ cmake -H. -B_build
$ cmake --build _build
$ ls _build/libformatter.a
```

### Part 2
```sh
$ cd ..
$ cd formatter_ex_lib
$ cat > CMakeLists.txt <<EOF
> cmake_minimum_required(VERSION 3.10)
> project(formatter_ex)
> EOF
$ cat > CMakeLists.txt <<EOF
> set(CMAKE_CXX_STANDARD 11)
> set(CMAKE_CXX_STANDARD_REQUIRED ON)
> set(CMAKE_CURRENT_SOURCE_DIR /home/nikitaklimov/STaRiCHDED/workspace/projects/HOMEWORK03/tmp/formatter_ex_lib)
> EOF
$ cat >> CMakeLists.txt <<EOF
> add_library(formatter_ex STATIC \${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex.cpp)
> EOF
$ cat >> CMakeLists.txt <<EOF
> include_directories(\${CMAKE_CURRENT_SOURCE_DIR})
> EOF
$ cat >> CMakeLists.txt <<EOF
> include_directories(/home/nikitaklimov/STaRiCHDED/workspace/projects/HOMEWORK03/tmp/formatter_lib)
> target_link_libraries(formatter_ex formatter)
> EOF
$ cmake -H. -B_build
$ cmake --build _build
$ cd ..
$ git remote remove origin
$ git remote add origin https://github.com/STaRiCHDED/HOMEWORK03.git
$ git add .
$ git commit -m"Homework03"
$ git push origin master
```
### Part 3
```sh
1.
$ cd hello_world_application
$ cat >CMakeLists.txt<<EOF
> cmake_minimum_required(VERSION 3.10)
> project(hello_world)
> 
> set(CMAKE_CXX_STANDARD 11)
> set(CMAKE_CXX_STANDARD_REQUIRED ON)
> set(CMAKE_CURRENT_SOURCE_DIR /home/nikitaklimov/STaRiCHDED/workspace/projects/HOMEWORK03/tmp)
> 
> add_executable(hello_world \${CMAKE_CURRENT_SOURCE_DIR}/hello_world_application/hello_world.cpp)
> 
> include_directories(\${CMAKE_CURRENT_SOURCE_DIR}/formatter_lib \${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex_lib)
> 
> add_library(hello STATIC /home/nikitaklimov/STaRiCHDED/workspace/projects/HOMEWORK03/tmp/formatter_ex_lib/formatter_ex.cpp /home/nikitaklimov/STaRiCHDED/workspace/projects/HOMEWORK03/tmp/formatter_lib/formatter.cpp)
> 
> target_link_libraries(hello_world hello)
> EOF
$ cmake -H. -B_build
$ cmake --build _build
$ _build/hello_world
-------------------------
hello, world!
-------------------------
2.
$ cd ..
$ cd solver_application
$ cat >CMakeLists.txt<<EOF
cmake_minimum_required(VERSION 3.10)
project(Solver)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CURRENT_SOURCE_DIR /home/nikitaklimov/STaRiCHDED/workspace/projects/HOMEWORK03/tmp)
add_executable(Solver ${CMAKE_CURRENT_SOURCE_DIR}/solver_application/equation.cpp)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/formatter_lib ${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex_lib ${CMAKE_CURRENT_SOURCE_DIR}/solver_lib)
add_library(solver STATIC /home/nikitaklimov/STaRiCHDED/workspace/projects/HOMEWORK03/tmp/solver_lib/solver.cpp 
/home/nikitaklimov/STaRiCHDED/workspace/projects/HOMEWORK03/tmp/formatter_ex_lib/formatter_ex.cpp 
/home/nikitaklimov/STaRiCHDED/workspace/projects/HOMEWORK03/tmp/formatter_lib/formatter.cpp)
target_link_libraries(Solver solver)
$ cmake -H. -B_build
$ cmake --build _build
$ _build/Solver
1
2
3
-------------------------
error: discriminant < 0
-------------------------

$ _build/Solver
1  
2
1
-------------------------
x1 = -1.000000
-------------------------
-------------------------
x2 = -1.000000
-------------------------
$ cd ..
$ git add .
$ git commit -a -m"HelloandSolve"
$ git push origin master
```

## Links
- [Основы сборки проектов на С/C++ при помощи CMake](https://eax.me/cmake/)
- [CMake Tutorial](http://neerc.ifmo.ru/wiki/index.php?title=CMake_Tutorial)
- [C++ Tutorial - make & CMake](https://www.bogotobogo.com/cplusplus/make.php)
- [Autotools](http://www.gnu.org/software/automake/manual/html_node/Autotools-Introduction.html)
- [CMake](https://cgold.readthedocs.io/en/latest/index.html)

```
Copyright (c) 2015-2020 The ISC Authors
```
