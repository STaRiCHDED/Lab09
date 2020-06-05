[![Build Status](https://travis-ci.com/STaRiCHDED/Lab09.svg?branch=master)](https://travis-ci.com/STaRiCHDED/Lab09)
## Laboratory work IX

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab09** на сервисе **GitHub**
- [x] 2. Ознакомиться со ссылками учебного материала
- [x] 3. Получить токен для доступа к репозиториям сервиса **GitHub**
- [x] 4. Выполнить инструкцию учебного материала
- [x] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**
## Tutorial
```sh
$ export GITHUB_TOKEN=8e2cdb55a74085a6a33c6b65de607324f84e226e
$ export GITHUB_USERNAME=STaRiCHDED
$ export PACKAGE_MANAGER=apt
$ export GPG_PACKAGE_NAME=gpg

$ $PACKAGE_MANAGER install xclip
$ alias gsed=sed
$ alias pbcopy='xclip -selection clipboard'
$ alias pbpaste='xclip -selection clipboard -o'

$ cd ${GITHUB_USERNAME}/workspace
$ pushd . 
$ source scripts/activate
$ go get github.com/aktau/github-release

$ git clone https://github.com/${GITHUB_USERNAME}/Lab08 projects/Lab09
$ cd projects/Lab09
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/Lab09

$ gsed -i "" 's/Lab08/Lab09/g' README.md

$ $PACKAGE_MANAGER install ${GPG_PACKAGE_NAME}
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Уже установлен пакет gpg самой новой версии (2.2.4-1ubuntu1.2).
gpg помечен как установленный вручную.
Следующие пакеты устанавливались автоматически и больше не требуются:
  libllvm8 libwayland-egl1-mesa
Для их удаления используйте «sudo apt autoremove».
Обновлено 0 пакетов, установлено 0 новых пакетов, для удаления отмечено 0 пакетов, и 143 пакетов не обновлено.
$ gpg --list-secret-keys --keyid-format LONG
$ gpg --full-generate-key
gpg (GnuPG) 2.2.4; Copyright (C) 2017 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Выберите тип ключа:
   (1) RSA и RSA (по умолчанию)
   (2) DSA и Elgamal
   (3) DSA (только для подписи)
   (4) RSA (только для подписи)
Ваш выбор? 1
открытый и секретный ключи созданы и подписаны.

pub   rsa3072 2020-06-05 [SC]
      247F7B1469B27BB5D5A823ECFD6BA86E3392F68E
uid          Klimov Nikita (Lab09) <nik179804@gmail.com>
sub   rsa3072 2020-06-05 [E]

$ gpg --list-secret-keys --keyid-format LONG
gpg: проверка таблицы доверия
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: глубина: 0  достоверных:   1  подписанных:   0  доверие: 0-, 0q, 0n, 0m, 0f, 1u
/home/nikitaklimov/.gnupg/pubring.kbx
------------------------------
sec   rsa3072/FD6BA86E3392F68E 2020-06-05 [SC]
      247F7B1469B27BB5D5A823ECFD6BA86E3392F68E
uid               [  абсолютно ] Klimov Nikita (Lab09) <nik179804@gmail.com>
ssb   rsa3072/D68738FFE8B04D4A 2020-06-05 [E]
$ gpg -K ${GITHUB_USERNAME}
sec   rsa3072 2020-06-05 [SC]
      247F7B1469B27BB5D5A823ECFD6BA86E3392F68E
uid               [  абсолютно ] Klimov Nikita (Lab09) <nik179804@gmail.com>
ssb   rsa3072 2020-06-05 [E]

$ GPG_KEY_ID=$(gpg --list-secret-keys --keyid-format LONG | grep ssb | tail -1 | awk '{print $2}' | awk -F'/' '{print $2}')
$ GPG_SEC_KEY_ID=$(gpg --list-secret-keys --keyid-format LONG | grep sec | tail -1 | awk '{print $2}' | awk -F'/' '{print $2}')
$ gpg --armor --export ${GPG_KEY_ID} | pbcopy
$ pbpaste
-----BEGIN PGP PUBLIC KEY BLOCK-----
.
.
.
-----END PGP PUBLIC KEY BLOCK-----
$ open https://github.com/settings/keys
$ git config user.signingkey ${GPG_SEC_KEY_ID}
$ git config gpg.program gpg
$ test -r ~/.zsh_profile && echo 'export GPG_TTY=$(tty)' >> ~/.zsh_profile
$ echo 'export GPG_TTY=$(tty)' >> ~/.profile
cmake -H. -B_build -DCPACK_GENERATOR="TGZ"
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
-- [hunter] Calculating Toolchain-SHA1
-- [hunter] Calculating Config-SHA1
-- [hunter] HUNTER_ROOT: /home/nikitaklimov/.hunter
-- [hunter] [ Hunter-ID: 5659b15 | Toolchain-ID: 9b2c9d4 | Config-ID: 8a1641b ]
-- [hunter] GTEST_ROOT: /home/nikitaklimov/.hunter/_Base/5659b15/9b2c9d4/8a1641b/Install (ver.: 1.10.0)
-- Looking for pthread.h
-- Looking for pthread.h - found
-- Looking for pthread_create
-- Looking for pthread_create - not found
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
-- Configuring done
-- Generating done
-- Build files have been written to: /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab09/_build
$ cmake --build _build --target package
Scanning dependencies of target print
[ 25%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 50%] Linking CXX static library libprint.a
[ 50%] Built target print
Scanning dependencies of target demo
[ 75%] Building CXX object CMakeFiles/demo.dir/demo/main.cpp.o
[100%] Linking CXX executable demo
[100%] Built target demo
Run CPack packaging tool...
CPack: Create package using TGZ
CPack: Install projects
CPack: - Run preinstall target for: print
CPack: - Install project: print
CPack: Create package
CPack: - package: /home/nikitaklimov/STaRiCHDED/workspace/projects/Lab09/_build/print-0.1.0.0-Linux.tar.gz generated.
travis login --auto
Successfully logged in as STaRiCHDED!
$ travis enable 
STaRiCHDED/Lab09: enabled :)

$ git tag -s v0.1.0.0
$ git tag -v v0.1.0.0
object d4h567mvfi154axy493lqodft3651vtaoct3764l
type commit
tag v0.1.0.0
tagger STaRiCHDED <nik179804@gmail.com> 1603296461 +0300

comment
gpg: Подпись сделана Пт 05 июн 2020 20:35:32 MSK
gpg:                ключом RSA с идентификатором 247F7B1469B27BB5D5A823ECFD6BA86E3392F68E
gpg: Действительная подпись пользователя "STaRiCHDED (Lab09) <nik179804@gmail.com>" [абсолютное]
$ git show v0.1.0.0tag v0.1.0.0
Tagger: STaRiCHDED <nik179804@gmail.com>
Date:   Fri Jun 5 20:36:05 2020 +0300

comment
-----BEGIN PGP SIGNATURE-----
.
.
.
-----END PGP SIGNATURE-----
commit d4h567mvfi154axy493lqodft3651vtaoct3764l (HEAD -> master,tag: v0.1.0.0)
Author: STaRiCHDED <73941730+STaRiCHDED@users.noreply.github.com>
Date:   Fri Jun 5 18:06:20 2020 +0300

$ git push origin master --tags
Username for 'https://github.com': STaRiCHDED
Password for 'https://STaRiCHDED@github.com': ************
Подсчет объектов: 228, готово.
Delta compression using up to 4 threads.
Сжатие объектов: 100% (129/129), готово.
Запись объектов: 100% (228/228), 1.84 MiB | 2.21 MiB/s, готово.
Total 228 (delta 86), reused 226 (delta 86)
remote: Resolving deltas: 100% (86/86), done.
To https://github.com/STaRiCHDED/Lab09
 * [new branch]      master -> master
 * [new tag]         v0.1.0.0 -> v0.1.0.0
 
 $ github-release --version
github-release v0.8.1
$ github-release info -u ${GITHUB_USERNAME} -r Lab09
tags:
- v0.1.0.0 (commit: https://api.github.com/repos/STaRiCHDED/Lab09/commits/d4h567mvfi154axy493lqodft3651vtaoct3764l)
releases:
$ github-release release \
    --user ${GITHUB_USERNAME} \
    --repo Lab09 \
    --tag v0.1.0.0 \
    --name "libprint" \
    --description "my first release"
$ export PACKAGE_OS=`uname -s` PACKAGE_ARCH=`uname -m`
$ export PACKAGE_FILENAME=print-${PACKAGE_OS}-${PACKAGE_ARCH}.tar.gz
$ github-release upload \
    --user ${GITHUB_USERNAME} \
    --repo Lab09 \
    --tag v0.1.0.0 \
    --name "${PACKAGE_FILENAME}" \
    --file _build/*.tar.gz
 $ github-release info -u ${GITHUB_USERNAME} -r Lab09tags:
- v0.1.0.0 (commit: https://api.github.com/repos/STaRiCHDED/Lab09/commits/d4h567mvfi154axy493lqodft3651vtaoct3764l)
releases:
- v0.1.0.0, name: 'libprint', description: 'my first release', id: 26326540, tagged: 05/06/2020 at 20:40, published: 05/06/2020 at 20:30, draft: ✗, prerelease: ✗
  - artifact: print-Darwin-x86_64.tar.gz, downloads: 0, state: uploaded, type: application/octet-stream, size: 20 kB, id: 20553497
$ wget https://github.com/${GITHUB_USERNAME}/Lab09/releases/download/v0.1.0.0/${PACKAGE_FILENAME}
--2020-06-05 20:50:40--  https://github.com/STaRiCHDED/Lab09/releases/download/v0.1.0.0/print-Darwin-x86_64.tar.gz
...
Сохранение в: «print-Darwin-x86_64.tar.gz»
print-Darwin-x86_64 100%[===================>]  19,44K   122KB/s    за 0,2s    
2020-06-05 19:51:57 (122 KB/s) - «print-Darwin-x86_64.tar.gz» сохранён [19909/19909]
# Просмотр содержимого архива
$ tar -ztf ${PACKAGE_FILENAME}
print-0.1.0.0-Darwin/cmake/
print-0.1.0.0-Darwin/cmake/print-config-noconfig.cmake
print-0.1.0.0-Darwin/cmake/print-config.cmake
print-0.1.0.0-Darwin/bin/
print-0.1.0.0-Darwin/bin/demo
print-0.1.0.0-Darwin/include/
print-0.1.0.0-Darwin/include/print.hpp
print-0.1.0.0-Darwin/lib/
print-0.1.0.0-Darwin/lib/libprint.a
```

## Report

```sh
$ popd
$ export LAB_NUMBER=09
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Links
- [BOOK](https://www.dockerbook.com/)
- [Instructions](https://docs.docker.com/engine/reference/builder/)
```
Copyright (c) 2015-2020 The ISC Authors
```
