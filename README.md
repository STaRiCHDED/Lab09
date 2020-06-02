## Laboratory work II

<a href="https://yandex.ru/efir/?stream_id=vMPJl0nEKr_0"><img src="https://raw.githubusercontent.com/tp-labs/lab02/master/preview.png" width="640"/></a>

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [X] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [X] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [X] 3. Ознакомиться со ссылками учебного материала
- [X] 4. Выполнить инструкцию учебного материала
- [X] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_USERNAME=STaRiCHDED
$ export GITHUB_EMAIL=nik179804@gmail.com
$ export GITHUB_TOKEN=*******************************
$ alias edit=subl
```

```sh
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate
```

```sh
$ mkdir ~/.config
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https
```

```sh
$ mkdir projects/lab02 && cd projects/lab02
$ git init
#Инициализирован пустой репозиторий Git в /home/nikitaklimov/STaRiCHDED/workspace/projects/lab02/.git/
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
# check your git global settings
$ git config -e --global
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
$ git pull origin master
remote: Enumerating objects: 93, done.
remote: Counting objects: 100% (93/93), done.
remote: Compressing objects: 100% (62/62), done.
remote: Total 93 (delta 30), reused 93 (delta 30), pack-reused 0
Распаковка объектов: 100% (93/93), готово.
Из https://github.com/STaRiCHDED/lab02
 * branch            master     -> FETCH_HEAD
 * [новая ветка]     master     -> origin/master

$ touch README.md
$ git status
$ git add README.md
$ git commit -m"added README.md"
$ git push origin master
Username for 'https://github.com': STaRiCHDED
Password for 'https://STaRiCHDED@github.com':************ 
Everything up-to-date
```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```sh
*build*/
*install*/
*.swp
.idea/
```

```sh
$ git pull origin master
remote: Enumerating objects: 8, done.
remote: Counting objects: 100% (8/8), done.
remote: Compressing objects: 100% (5/5), done.
remote: Total 6 (delta 2), reused 0 (delta 0), pack-reused 0
Распаковка объектов: 100% (6/6), готово.
Из https://github.com/STaRiCHDED/lab02
 * branch            master     -> FETCH_HEAD
   af8687b..03a465e  master     -> origin/master
Обновление af8687b..03a465e
Fast-forward
 .gitignore |  4 ++++
 README.md  | 31 ++++++++++++++++++++++---------
 2 files changed, 26 insertions(+), 9 deletions(-)
 create mode 100644 .gitignore
$ git log
commit 03a465e6bccff4290d1df0b1ee0a46e88e535366 (HEAD -> master, origin/master)
Author: STaRiCHDED <61161128+STaRiCHDED@users.noreply.github.com>
Date:   Tue Jun 2 16:28:25 2020 +0300

    Create .gitignore

commit 90d660b8d31edbf44eb784cb65981235b975e7d5
Author: STaRiCHDED <61161128+STaRiCHDED@users.noreply.github.com>
Date:   Tue Jun 2 16:21:21 2020 +0300

    Update README.md
```

```sh
$ mkdir sources
$ mkdir include
$ mkdir examples
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```

```sh
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```sh
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```sh
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```sh
$ edit README.md
```

```sh
$ git status
На ветке master
Неотслеживаемые файлы:
  (используйте «git add <файл>…», чтобы добавить в то, что будет включено в коммит)

	examples/
	include/
	sources/

ничего не добавлено в коммит, но есть неотслеживаемые файлы (используйте «git add», чтобы отслеживать их)
$ git add .
$ git commit -m"added sources"
[master d54cb89] added sources
 4 files changed, 32 insertions(+)
 create mode 100644 examples/example1.cpp
 create mode 100644 examples/example2.cpp
 create mode 100644 include/print.hpp
 create mode 100644 sources/print.cpp
$ git push origin master
Username for 'https://github.com': STaRiCHDED
Password for 'https://STaRiCHDED@github.com':************ 
Подсчет объектов: 9, готово.
Delta compression using up to 8 threads.
Сжатие объектов: 100% (7/7), готово.
Запись объектов: 100% (9/9), 1002 bytes | 334.00 KiB/s, готово.
Total 9 (delta 0), reused 0 (delta 0)
remote: This repository moved. Please use the new location:
remote:   https://github.com/STaRiCHDED/Lab02.git
To https://github.com/STaRiCHDED/lab02.git
   03a465e..d54cb89  master -> master
```

## Report

```sh
$ cd ~/STaRiCHDED/workspace/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
4. Добавьте этот файл в локальную копию репозитория.
5. Закоммитьте изменения с *осмысленным* сообщением.
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
8. Запуште изменения в удалёный репозиторий.
9. Проверьте, что история коммитов доступна в удалёный репозитории.

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
3. **commit**, **push** локальную ветку в удалённый репозиторий.
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
5. Создайте pull-request `patch1 -> master`.
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
7. **commit**, **push**.
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
10. Локально выполните **pull**.
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
12. Удалите локальную ветку `patch1`.

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
7. Сделайте *force push* в ветку `patch2`
8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2020 The ISC Authors
```
