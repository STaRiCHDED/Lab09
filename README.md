
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
