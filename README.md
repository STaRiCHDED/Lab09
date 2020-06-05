[![Build Status](https://travis-ci.com/STaRiCHDED/Lab07.svg?branch=master)](https://travis-ci.com/STaRiCHDED/Lab07)
## Laboratory work VII
## Tutorial
```sh
$ export GITHUB_USERNAME=STaRiCHDED
$ alias gsed=sed
$  cd ${GITHUB_USERNAME}/workspace
$ pushd .
~/STaRiCHDED/workspace ~/STaRiCHDED/workspace
$ source scripts/activate
$ git clone https://github.com/${GITHUB_USERNAME}/Lab06 projects/Lab07
Клонирование в «projects/Lab07»…
remote: Enumerating objects: 190, done.
remote: Counting objects: 100% (190/190), done.
remote: Compressing objects: 100% (107/107), done.
remote: Total 190 (delta 77), reused 185 (delta 75), pack-reused 0
Получение объектов: 100% (190/190), 1.71 MiB | 528.00 KiB/s, готово.
Определение изменений: 100% (77/77), готово.
$ cd projects/Lab07
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/Lab07
$ mkdir -p cmake
$ wget https://raw.githubusercontent.com/cpp-pm/gate/master/cmake/HunterGate.cmake -O cmake/HunterGate.cmake
--2020-06-05 12:08:46--  https://raw.githubusercontent.com/cpp-pm/gate/master/cmake/HunterGate.cmake
Распознаётся raw.githubusercontent.com (raw.githubusercontent.com)… 151.101.84.133
Подключение к raw.githubusercontent.com (raw.githubusercontent.com)|151.101.84.133|:443... соединение установлено.
HTTP-запрос отправлен. Ожидание ответа… 200 OK
Длина: 17070 (17K) [text/plain]
Сохранение в: «cmake/HunterGate.cmake»

cmake/HunterGate.cmake    100%[==================================>]  16,67K  --.-KB/s    за 0,03s   

2020-06-05 12:08:47 (500 KB/s) - «cmake/HunterGate.cmake» сохранён [17070/17070]

$ gsed -i '/cmake_minimum_required(VERSION 3.4)/a\
> \
> include("cmake/HunterGate.cmake")\
> HunterGate(\
>     URL "https://github.com/cpp-pm/hunter/archive/v0.23.251.tar.gz"\
>    SHA1 "5659b15dc0884d4b03dbd95710e6a1fa0fc3258d"\
> )\
> ' CMakeLists.txt
$ git rm -rf third-party/gtest
rm 'third-party/gtest'
$ gsed -i '/set(PRINT_VERSION_STRING "v\${PRINT_VERSION}")/a\
> \
> hunter_add_package(GTest)\
> find_package(GTest CONFIG REQUIRED)\
> ' CMakeLists.txt
$  gsed -i 's/add_subdirectory(third-party/gtest)//' CMakeLists.txt
$ gsed -i 's/gtest_main/GTest::gtest_main/' CMakeLists.txt
$ cmake -H. -B_builds -DBUILD_TESTS=ON
-- [hunter] Initializing Hunter workspace (5659b15dc0884d4b03dbd95710e6a1fa0fc3258d)
-- [hunter]   https://github.com/cpp-pm/hunter/archive/v0.23.251.tar.gz
-- [hunter]   -> /home/nikitaklimov/.hunter/_Base/Download/Hunter/0.23.251/5659b15
$  cmake --build _builds
Scanning dependencies of target print
[ 25%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 50%] Linking CXX static library libprint.a
[ 50%] Built target print
Scanning dependencies of target check
[ 75%] Building CXX object CMakeFiles/check.dir/tests/test1.cpp.o
[100%] Linking CXX executable check
[100%] Built target check
$  cmake --build _builds --target test
Running tests...
Test project /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab07/_builds
    Start 1: check
1/1 Test #1: check ............................   Passed    0.00 sec

100% tests passed, 0 tests failed out of 1

Total Test time (real) =   0.00 sec
$ ls -la $HOME/.hunter
итого 12
drwxr-xr-x  3 nikitaklimov nikitaklimov 4096 июн  5 12:15 .
drwxr-xr-x 26 nikitaklimov nikitaklimov 4096 июн  5 12:15 ..
drwxr-xr-x  6 nikitaklimov nikitaklimov 4096 июн  5 12:15 _Base
$ git clone https://github.com/cpp-pm/hunter $HOME/projects/hunter
Клонирование в «/home/nikitaklimov/projects/hunter»…
remote: Enumerating objects: 44585, done.
remote: Total 44585 (delta 0), reused 0 (delta 0), pack-reused 44585
Получение объектов: 100% (44585/44585), 11.25 MiB | 1.56 MiB/s, готово.
Определение изменений: 100% (28245/28245), готово.
$ export HUNTER_ROOT=$HOME/projects/hunter
$ rm -rf _builds
$ cmake -H. -B_builds -DBUILD_TESTS=ON
-- The C compiler identification is GNU 7.5.0
-- The CXX compiler identification is GNU 7.5.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
...............................................
$ cmake --build _builds
Scanning dependencies of target print
[ 25%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 50%] Linking CXX static library libprint.a
[ 50%] Built target print
Scanning dependencies of target check
[ 75%] Building CXX object CMakeFiles/check.dir/tests/test1.cpp.o
[100%] Linking CXX executable check
[100%] Built target check
$  cmake --build _builds --target test
Running tests...
Test project /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab07/_builds
    Start 1: check
1/1 Test #1: check ............................   Passed    0.00 sec

100% tests passed, 0 tests failed out of 1

Total Test time (real) =   0.00 sec
$  cat $HUNTER_ROOT/cmake/configs/default.cmake | grep GTest
  hunter_default_version(GTest VERSION 1.7.0-hunter-6)
  hunter_default_version(GTest VERSION 1.10.0)
$  cat $HUNTER_ROOT/cmake/projects/GTest/hunter.cmake
# Copyright (c) 2013, Ruslan Baratov
# All rights reserved.
..............................................
$ mkdir cmake/Hunter
$ cat > cmake/Hunter/config.cmake <<EOF
> hunter_config(GTest VERSION 1.7.0-hunter-9)
> EOF
$ mkdir demo
$ cat > demo/main.cpp <<EOF
> #include <print.hpp>
>  #include <cstdlib>
> int main(int argc, char* argv[])
> {
> const char* log_path = std::getenv("LOG_PATH");
> if (log_path == nullptr)
> {
>  std::cerr << "undefined environment variable: LOG_PATH" << std::endl;
> return 1;
> }
> std::string text;
> while (std::cin >> text)
>  {
> std::ofstream out{log_path, std::ios_base::app};
>  print(text, out);
>  out << std::endl;
>  }
> }
> EOF
$ gsed -i '/endif()/a\
> \
> add_executable(demo ${CMAKE_CURRENT_SOURCE_DIR}/demo/main.cpp)\
> target_link_libraries(demo print)\
> install(TARGETS demo RUNTIME DESTINATION bin)\
> ' CMakeLists.txt
$ mkdir tools
$ git submodule add https://github.com/ruslo/polly tools/polly
Клонирование в «/home/nikitaklimov/STaRiCHDED/workspace/projects/Lab07/tools/polly»…
remote: Enumerating objects: 29, done.
remote: Counting objects: 100% (29/29), done.
remote: Compressing objects: 100% (19/19), done.
remote: Total 6423 (delta 10), reused 24 (delta 10), pack-reused 6394
Получение объектов: 100% (6423/6423), 1.64 MiB | 355.00 KiB/s, готово.
Определение изменений: 100% (4418/4418), готово.
$ tools/polly/bin/polly.py --test
Python version: 3.6
Build dir: /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab07/_builds/default
Execute command: [
  `which`
  `cmake`
]
.............................................
Log saved: /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab07/_logs/polly/default/log.txt
-
Generate: 0:00:05.693706s
Build: 0:00:02.103042s
Test: 0:00:00.021691s
-
Total: 0:00:07.818669s
-
SUCCESS
$ tools/polly/bin/polly.py --install
Python version: 3.6
Build dir: /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab07/_builds/default
Execute command: [
  `which`
  `cmake`
]

[/home/nikitaklimov/STaRiCHDED/workspace/projects/Lab07]> "which" "cmake"

/usr/bin/cmake
Execute command: [
  `cmake`
  `--version`
]

[/home/nikitaklimov/STaRiCHDED/workspace/projects/Lab07]> "cmake" "--version"

cmake version 3.10.2

CMake suite maintained and supported by Kitware (kitware.com/cmake).

== WARNING ==

Looks like cmake arguments changed. You have two options to fix it:
  * Remove build directory completely by adding '--clear' (works 100%)
  * Run configure again by adding '--reconfig' (you must understand how CMake cache variables works/updated)

- "cmake" "-H." "-B/home/nikitaklimov/STaRiCHDED/workspace/projects/Lab07/_builds/default" "-DCMAKE_TOOLCHAIN_FILE=/home/nikitaklimov/STaRiCHDED/workspace/projects/Lab07/tools/polly/default.cmake"
+ "cmake" "-H." "-B/home/nikitaklimov/STaRiCHDED/workspace/projects/Lab07/_builds/default" "-DCMAKE_TOOLCHAIN_FILE=/home/nikitaklimov/STaRiCHDED/workspace/projects/Lab07/tools/polly/default.cmake" "-DCMAKE_INSTALL_PREFIX=/home/nikitaklimov/STaRiCHDED/workspace/projects/Lab07/_install/default"
?      
$ tools/polly/bin/polly.py --toolchain clang-cxx14
Python version: 3.6
Build dir: /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab07/_builds/clang-cxx14
Execute command: [
  `which`
  `cmake`
]
.............................................................
Log saved: /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab07/_logs/polly/clang-cxx14/log.txt
-
Generate: 0:00:43.900880s
Build: 0:00:02.292085s
-
Total: 0:00:46.193172s
-
SUCCESS
$ git add .
$ git commit -m"Lab07"
[master fa65426] Lab07
10 files changed, 1039 insertions(+), 6 deletions(-)
create mode 100644 _logs/polly/clang-cxx14/log.txt
create mode 100644 _logs/polly/default/log-0.txt
create mode 100644 _logs/polly/default/log.txt
create mode 100644 cmake/Hunter/config.cmake
create mode 100644 cmake/HunterGate.cmake
create mode 100644 demo/main.cpp
delete mode 160000 third-party/gtest
create mode 160000 tools/polly
$ git push origin master
Username for 'https://github.com': STaRiCHDED
Password for 'https://STaRiCHDED@github.com': 
Подсчет объектов: 208, готово.
Delta compression using up to 8 threads.
Сжатие объектов: 100% (117/117), готово.
Запись объектов: 100% (208/208), 1.72 MiB | 1.78 MiB/s, готово.
Total 208 (delta 80), reused 188 (delta 77)
remote: Resolving deltas: 100% (80/80), done.
To https://github.com/STaRiCHDED/Lab07
 * [new branch]      master -> master


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
