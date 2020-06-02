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


## Homework

### Part I
```sh
1.
2.
$ mkdir homework02
$ cd homework02
$ subl README.md
$ echo "# homework02" >> README.md
$ git init
Инициализирован пустой репозиторий Git в /home/nikitaklimov/STaRiCHDED/workspace/reports/homework02/.git/
$ git add README.md
$ git commit -m "first commit"
[master (корневой коммит) bfde725] first commit
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
 $ git remote add origin https://github.com/STaRiCHDED/homework02.git
 $ git push -u origin master
Username for 'https://github.com': STaRiCHDED
Password for 'https://STaRiCHDED@github.com':************ 
Подсчет объектов: 3, готово.
Запись объектов: 100% (3/3), 228 bytes | 228.00 KiB/s, готово.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/STaRiCHDED/homework02.git
 * [new branch]      master -> master
Ветка «master» отслеживает внешнюю ветку «master» из «origin».
3.
$ cat > hello_world.cpp <<EOF
> #include <iosrteam>
> 
> using namespase std;
> 
> int main()
> {
> cout << "Hello, world!" << endl;
> return 0;
> }
> EOF
4.
$ git add .
5.
$ git commit -m"added hello_world.cpp"
 hello_world.cpp"
[master 4f2c604] added hello_world.cpp
1 file changed, 9 insertions(+)
create mode 100644 hello_world.cpp/hello_world.cpp
6.
7.
$ git commit -a -m "Update hello_world.cpp"
[master d534c12] Update hello_world.cpp
1 file changed, 7 insertions(+), 6 deletions(-)
8.
$ git push origin master
Username for 'https://github.com': STaRiCHDED
Password for 'https://STaRiCHDED@github.com': 
Подсчет объектов: 8, готово.
Delta compression using up to 8 threads.
Сжатие объектов: 100% (6/6), готово.
Запись объектов: 100% (8/8), 883 bytes | 441.00 KiB/s, готово.
Total 8 (delta 0), reused 0 (delta 0)
To https://github.com/STaRiCHDED/homework02.git
   bfde725..d534c12  master -> master
```

### Part II
```sh
1.
$ git branch patch1
$ git checkout patch1
Переключено на ветку «patch1»
2.
$ subl hello_world.cpp
$ cat > hello_world.cpp <<EOF
> #include <iosrteam>
> int main()
> {
>     std::string name;
>     getline(cin, name);
>     std::cout << "Hello world from " << name << std::endl;
>     return 0;
> }
> EOF
3.
$ git add .
$ git commit -m"added1 hello_world.cpp"
[patch1 1e8055c] added1 hello_world.cpp
 1 file changed, 5 insertions(+), 7 deletions(-)
 $ git push origin patch1
Username for 'https://github.com': STaRiCHDED
Password for 'https://STaRiCHDED@github.com':************ 
Подсчет объектов: 15, готово.
Delta compression using up to 8 threads.
Сжатие объектов: 100% (10/10), готово.
Запись объектов: 100% (15/15), 1.48 KiB | 1.48 MiB/s, готово.
Total 15 (delta 0), reused 0 (delta 0)
remote: 
remote: Create a pull request for 'patch1' on GitHub by visiting:
remote:      https://github.com/STaRiCHDED/homework02/pull/new/patch1
remote: 
To https://github.com/STaRiCHDED/homework02.git
 * [new branch]      patch1 -> patch1
 4.
 5.
 6.
 $ cat > hello_world.cpp <<EOF
> #include <iosrteam> //Создаём программу
> int main()
> {
>     std::string name;
>     getline(cin, name);
>     std::cout << "Hello world from " << name << std::endl;
>     return 0;
> } //Программа завершила работу
> EOF
7.
$ git commit -a -m"added1 hello_world.cpp"
[patch1 8899416] added1 hello_world.cpp
1 file changed, 6 insertions(+), 6 deletions(-)
$ git push origin patch1
Username for 'https://github.com': STaRiCHDED
Password for 'https://STaRiCHDED@github.com': 
Подсчет объектов: 3, готово.
Delta compression using up to 8 threads.
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (3/3), 483 bytes | 483.00 KiB/s, готово.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/STaRiCHDED/HOMEWORK02.git
c88e641..8899416  patch1 -> patch1
8.
9.
10.
git checkout master
Переключено на ветку «master»
Ваша ветка обновлена в соответствии с «origin/master».
$ git merge patch1
Обновление a1a41d1..8899416
Fast-forward
 hello_world.cpp | 14 ++++++--------
 1 file changed, 6 insertions(+), 8 deletions(-)
 11.
 $ git log
commit 8899416fcdbf9dcd292fdd6506208a5b09a0e41d (HEAD -> master, origin/patch1, patch1)
Author: STaRiCHDED <nik179804@gmail.com>
Date:   Tue Jun 2 22:30:32 2020 +0300

    added1 hello_world.cpp

commit c88e6419a05732d0dda8ab71ae2d6ecc16d2d27b
Author: STaRiCHDED <nik179804@gmail.com>
Date:   Tue Jun 2 22:20:56 2020 +0300

    added1 hello_world.cpp

commit a1a41d10ed9b8169b39fbb48a33a38c2252fde6b (origin/master)
Author: STaRiCHDED <nik179804@gmail.com>
Date:   Tue Jun 2 22:14:42 2020 +0300

    Update hello_world.cpp

commit 338ae9310c0f674b270daec3bb9305c2a13b521c
Author: STaRiCHDED <nik179804@gmail.com>
Date:   Tue Jun 2 22:12:06 2020 +0300

    added hello_world.cpp

commit e475970639030df71e2c75bca5d9177d7a0be9ef
Author: STaRiCHDED <nik179804@gmail.com>
Date:   Tue Jun 2 22:08:26 2020 +0300
12.
$ git branch -d patch1
Ветка patch1 удалена (была 8899416).
```
### Part III
```sh
1.
$ git branch patch2
$ git checkout patch2
Переключено на ветку «patch2»
2.
$ clang-format -style=Mozilla -i hello_world.cpp
3.
$ git add .
$ git commit -m"added2 hello_world.cpp"
[patch2 7004db4] added2 hello_world.cpp
 1 file changed, 6 insertions(+), 5 deletions(-)
$ git push origin patch2
Username for 'https://github.com': STaRiCHDED
Password for 'https://STaRiCHDED@github.com': 
Подсчет объектов: 18, готово.
Delta compression using up to 8 threads.
Сжатие объектов: 100% (16/16), готово.
Запись объектов: 100% (18/18), 2.05 KiB | 2.05 MiB/s, готово.
Total 18 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
remote: 
remote: Create a pull request for 'patch2' on GitHub by visiting:
remote:      https://github.com/STaRiCHDED/HOMEWORK02/pull/new/patch2
remote: 
To https://github.com/STaRiCHDED/HOMEWORK02.git
 * [new branch]      patch2 -> patch2
4.
5.
6.
$git checkout master
$ git pull origin master
$ git checkout patch2
$ git rebase master # Конфликт слияния
$ edit hello_world.cpp # Ручное разрешение конфликта
$ git add hello_world.cpp
$ git commit -m "Fix conflicts"
$ git rebase --continue
$ git checkout master
$ git merge patch2 
7.
git push -f origin patch2
8.
9.
```

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2020 The ISC Authors
```
