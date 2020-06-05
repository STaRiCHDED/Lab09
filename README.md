[![Build Status](https://travis-ci.com/STaRiCHDED/Lab08.svg?branch=master)](https://travis-ci.com/STaRiCHDED/Lab08)
## Laboratory work VIII
## Tutorial
```sh
$ export GITHUB_USERNAME=STaRiCHDED
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
$ source scripts/activate
$ git clone https://github.com/${GITHUB_USERNAME}/Lab07 projects/Lab08
Клонирование в «projects/Lab08»…
remote: Enumerating objects: 220, done.
remote: Counting objects: 100% (220/220), done.
remote: Compressing objects: 100% (126/126), done.
remote: Total 220 (delta 88), reused 206 (delta 80), pack-reused 0
Получение объектов: 100% (220/220), 1.73 MiB | 1.38 MiB/s, готово.
Определение изменений: 100% (88/88), готово.
$ cd projects/Lab08
$ git submodule update --init
Подмодуль «tools/polly» (https://github.com/ruslo/polly) зарегистрирован по пути «tools/polly»
Клонирование в «/home/nikitaklimov/STaRiCHDED/workspace/projects/Lab08/tools/polly»…
Подмодуль по пути «tools/polly»: забрано состояние «0b3806e193b668fbb9b70c9aa70735b29396323d»
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/Lab08
$ cat > Dockerfile <<EOF
> FROM ubuntu:18.04
> EOF
$ cat >> Dockerfile <<EOF
> 
> RUN apt update
> RUN apt install -yy gcc g++ cmake
> EOF
$ cat >> Dockerfile <<EOF
> 
> COPY . print/
> WORKDIR print
> EOF
$ cat >> Dockerfile <<EOF
> 
> RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
> RUN cmake --build _build
> RUN cmake --build _build --target install
> EOF
$ cat >> Dockerfile <<EOF
> 
> ENV LOG_PATH /home/logs/log.txt
> EOF
$ cat >> Dockerfile <<EOF
> 
> VOLUME /home/logs
> EOF
$ cat >> Dockerfile <<EOF
> 
> WORKDIR _install/bin
> EOF
$ cat >> Dockerfile <<EOF
> 
> ENTRYPOINT ./demo
> EOF
$ docker build -t logger .
Sending build context to Docker daemon   7.55MB
Step 1/12 : FROM ubuntu:18.04
 ---> c3c304cb4f22
Step 2/12 : RUN apt update
 ---> Using cache
 ---> 48a18c916b46
Step 3/12 : RUN apt install -yy gcc g++ cmake
 ---> Using cache
 ---> 023817954882
Step 4/12 : COPY . print/
 ---> b066973370ef
Step 5/12 : WORKDIR print
 ---> Running in 8b1852ec40e4
Removing intermediate container 8b1852ec40e4
 ---> 4e2c31b5e590
Step 6/12 : RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
 ---> Running in cb2e4ab0680a
Step 7/12 : RUN cmake --build _build
 ---> Running in f5706a746195
Scanning dependencies of target print
[ 25%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 50%] Linking CXX static library libprint.a
[ 50%] Built target print
Scanning dependencies of target demo
[ 75%] Building CXX object CMakeFiles/demo.dir/demo/main.cpp.o
[100%] Linking CXX executable demo
[100%] Built target demo
Removing intermediate container f5706a746195
 ---> 751455497198
Step 8/12 : RUN cmake --build _build --target install
 ---> Running in 0b563cea333b
[ 50%] Built target print
[100%] Built target demo
Install the project...
-- Install configuration: "Release"
-- Installing: /print/_install/lib/libprint.a
-- Installing: /print/_install/include
-- Installing: /print/_install/include/print.hpp
-- Installing: /print/_install/cmake/print-config.cmake
-- Installing: /print/_install/cmake/print-config-release.cmake
-- Installing: /print/_install/bin/demo
Removing intermediate container 0b563cea333b
 ---> 09fc6f5389a3
Step 9/12 : ENV LOG_PATH /home/logs/log.txt
 ---> Running in 09931879c8ca
Removing intermediate container 09931879c8ca
 ---> 5ae633ba2e7f
Step 10/12 : VOLUME /home/logs
 ---> Running in 4c6bc3cb3717
Removing intermediate container 4c6bc3cb3717
 ---> c5954059f2a4
Step 11/12 : WORKDIR _install/bin
 ---> Running in d8d9fa331365
Removing intermediate container d8d9fa331365
 ---> 99aebe810952
Step 12/12 : ENTRYPOINT ./demo
 ---> Running in 4bd8aca15bdb
Removing intermediate container 4bd8aca15bdb
 ---> 3a7da5174d63
Successfully built 3a7da5174d63
Successfully tagged logger:latest
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
logger              latest              3a7da5174d63        12 seconds ago      346MB
<none>              <none>              4aae51cb1a27        18 minutes ago      346MB
<none>              <none>              c8684c94a0fe        30 minutes ago      346MB
<none>              <none>              d01570a0bfff        38 minutes ago      346MB
ubuntu              18.04               c3c304cb4f22        6 weeks ago         64.2MB
hello-world         latest              bf756fb1ae65        5 months ago        13.3kB
$ mkdir logs
$ docker run -it -v "$(pwd)/logs/:/home/logs/" logger
text1
text2
text3
$ docker inspect logger
[
    {
        "Id": "sha256:3a7da5174d63c936ed908441f2968099af3c734fb0ba16cfe431f0ed148f6298",
        "RepoTags": [
            "logger:latest"
        ],
        "RepoDigests": [],
        "Parent": "sha256:99aebe81095275c6b5f9b73110fec486f00a5fd0c18074b73c4f6964de556142",
        "Comment": "",
        "Created": "2020-06-05T14:12:57.01031651Z",
        "Container": "4bd8aca15bdbc8912968c24975da491f800dbea8afcab6de95a35fc472111c81",
        "ContainerConfig": {
            "Hostname": "4bd8aca15bdb",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "LOG_PATH=/home/logs/log.txt"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "#(nop) ",
                "ENTRYPOINT [\"/bin/sh\" \"-c\" \"./demo\"]"
            ],
            "Image": "sha256:99aebe81095275c6b5f9b73110fec486f00a5fd0c18074b73c4f6964de556142",
            "Volumes": {
                "/home/logs": {}
            },
            "WorkingDir": "/print/_install/bin",
            "Entrypoint": [
                "/bin/sh",
                "-c",
                "./demo"
            ],
            "OnBuild": null,
            "Labels": {}
        },
        "DockerVersion": "19.03.6",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "LOG_PATH=/home/logs/log.txt"
            ],
            "Cmd": null,
            "Image": "sha256:99aebe81095275c6b5f9b73110fec486f00a5fd0c18074b73c4f6964de556142",
            "Volumes": {
                "/home/logs": {}
            },
            "WorkingDir": "/print/_install/bin",
            "Entrypoint": [
                "/bin/sh",
                "-c",
                "./demo"
            ],
            "OnBuild": null,
            "Labels": null
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 345581033,
        "VirtualSize": 345581033,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/d1497d9d3afecce403e3c8d7f1f57b268b84363e697a74bc303446408600f579/diff:/var/lib/docker/overlay2/355c12b3bbce15b6d23e9759487a4cf7a9d98bd1dd0f59322ce3b04ad414e1c2/diff:/var/lib/docker/overlay2/8b89ed4ef86c8f688498f729626007c710fd652893d2ae904ac9698b035a78bc/diff:/var/lib/docker/overlay2/97616490c691b40a4425cabe0f2551348a5b19212e109cb7b510d0f3a7ceed91/diff:/var/lib/docker/overlay2/dbb7becf67083a0b83de95e8744109350c50347a43eb3e334648a265c075b165/diff:/var/lib/docker/overlay2/0f58d60bd09299a180945f6784dd0b86f020ac8f2a64e42e4c7b78c795145841/diff:/var/lib/docker/overlay2/e49f617dae5aff6b950ecdd92d00bc8b072bb1e3ab81916e75a03b8dd53e840a/diff:/var/lib/docker/overlay2/d92f50c4f04f85d4b3c755cdcd04d61d1aed1f3a13663b38760cdb062dddea66/diff:/var/lib/docker/overlay2/b92250dd2cacb8c15dcdef657af0953582f5a7b19bb24e72427ed6704e20aa45/diff",
                "MergedDir": "/var/lib/docker/overlay2/4104ebd79f396774f5042101540ef49d0405d5e4986d48115187d75c56cd37aa/merged",
                "UpperDir": "/var/lib/docker/overlay2/4104ebd79f396774f5042101540ef49d0405d5e4986d48115187d75c56cd37aa/diff",
                "WorkDir": "/var/lib/docker/overlay2/4104ebd79f396774f5042101540ef49d0405d5e4986d48115187d75c56cd37aa/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:b7f7d2967507ba709dbd1dd0426a5b0cdbe1ff936c131f8958c8d0f910eea19e",
                "sha256:a6ebef4a95c345c844c2bf43ffda8e36dd6e053887dd6e283ad616dcc2376be6",
                "sha256:838a37a24627f72df512926fc846dd97c93781cf145690516e23335cc0c27794",
                "sha256:28ba7458d04b8551ff45d2e17dc2abb768bf6ed1a46bb262f26a24d21d8d7233",
                "sha256:50e6d3fb5c986d686746bc6ecf89ed34fb5e03989e60c97861a523ee2cc63c47",
                "sha256:345e91c68359a5f443a6de6b4e2ba2bda3decf210cde343ca3fe174c0e13f2c0",
                "sha256:95a95cc0bb65c1b8be2af5187ae95d34075d5e4bb4d1b4d3bf085784317d6bf7",
                "sha256:a7d5eedb8fa767864270fdf125c718e7c467290fa216663a234bbd86f9218050",
                "sha256:90a60111c6b1e012603e872623be3f99d56b6b205f78ad934688d12bad8705ec",
                "sha256:7456d34aa35d0c2cc3dfe9f04d4bcf0412d0707198bcf18a42bf8f77af25d19e"
            ]
        },
        "Metadata": {
            "LastTagTime": "2020-06-05T17:12:57.070683917+03:00"
        }
    }
]
$ cat logs/log.txt
text1
text2
text3
$ sed -i 's/Lab07/Lab08/g' README.md
$ git add Dockerfile
$ git add .travis.yml
$ git add README.md
$ git commit -m"adding Dockerfile"
[master 3541cd0] adding Dockerfile
 3 files changed, 43 insertions(+), 34 deletions(-)
 create mode 100644 Dockerfile
$ git push origin master
Username for 'https://github.com': STaRiCHDED
Password for 'https://STaRiCHDED@github.com': 
Подсчет объектов: 225, готово.
Delta compression using up to 8 threads.
Сжатие объектов: 100% (123/123), готово.
Запись объектов: 100% (225/225), 1.73 MiB | 2.13 MiB/s, готово.
Total 225 (delta 90), reused 219 (delta 88)
remote: Resolving deltas: 100% (90/90), done.
To https://github.com/STaRiCHDED/Lab08
 * [new branch]      master -> master
$ travis login --auto
$ travis enable
```

## Report

```sh
$ popd
$ export LAB_NUMBER=08
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
