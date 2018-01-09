+++
title = "Docker"
+++

## はじめに

公式ドキュメントを最初に読むこと。
https://docs.docker.com/

学べること
1. Dockerコンテナの基本的な使い方
2. Docker Serviceの使い方
3. Docker Swarmの使い方

## 各種確認コマンド

* `docker ps` ... 現在動いているコンテナ情報を確認できる

```bash
$ docker ps
CONTAINER ID        IMAGE                   COMMAND               CREATED             STATUS              PORTS                   NAMES
c2725ccd7681        nikuyoshi/ssh:centos7   "/usr/sbin/sshd -D"   6 minutes ago       Up 6 minutes        0.0.0.0:32768->22/tcp   elated_hoover
```

* `docker exec` ... 対象のコンテナに対してコマンド実行

```bash
$ docker exec -u 0 -it [contair id] bash
[root@[container id] /]#
```

* `docker build`

`docker build` をする際、Dockerfileの場所を明示的に書く。

```bash
$ ll
total 72
-rw-r--r--  1 nikuyoshi  staff   562B  6 19 01:43 Dockerfile
-rw-r--r--  1 nikuyoshi  staff    18K  6 19 01:43 LICENSE
-rw-r--r--  1 nikuyoshi  staff   648B  6 19 01:43 README.md
-rw-r--r--  1 nikuyoshi  staff   177B  6 19 01:43 cccp.yml
-rw-r--r--  1 nikuyoshi  staff   236B  6 19 01:43 start.sh
$ centos7 [master] docker build --rm -t nikuyoshi/ssh:centos7 .

```

## これしたい

### CentOSを立ててsshでログインして操作したい

以下のリポジトリを参照する。(Cent OS版)

https://github.com/CentOS/CentOS-Dockerfiles/tree/master/ssh

ID, Passwordはstart.sh内に記載あり

rootでログインしてコマンド叩きたい場合は以下の通り。 [参考](https://stackoverflow.com/questions/30172605/how-to-get-into-a-docker-container)

```bash
$ docker exec -u 0 -it [container id] bash
```

`yum install` で必要なコマンドがなかったら適宜EPELをインストールすること。

```bash
$ sudo yum install epel-release
```

