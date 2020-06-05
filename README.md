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

## Report

```sh
$ popd
$ export LAB_NUMBER=07
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
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
