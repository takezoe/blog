---
layout: post
title:  "boot2dockerでMacでDockerを使ってみる"
date: 2014-06-28 22:06:00
categories: mac, docker
---

今までWindows上でVagrantでVirtualBox上のUbuntuにDockerをインストールして動かしていたのですが、自宅のMacBook ProにもDocker環境を作ってみようと思い、Dockerの公式サイトでも紹介されていた[boot2docker](https://github.com/boot2docker/boot2docker)をインストールしてみました。

インストールは非常に簡単で、[Mac用のインストーラ](https://github.com/boot2docker/osx-installer/releases)をダウンロードしてインストールするだけです。boot2dockerはDockerを直接Mac上で実行するわけではなく、仮想マシン上のLinuxで実行するものですが、boot2dockerのインストーラでVirtualBoxも一緒にインストールされるので非常にお手軽です。

あとはアプリケーションからboot2docker.appを実行するか、ターミナルから以下のコマンドを実行するとDockerを利用可能になります。

```bash
$ boot2docker init
$ boot2docker start
$ export DOCKER_HOST=tcp://$(boot2docker ip 2>/dev/null):2375
```

この状態でVirtualBoxのコンソールを起動すると以下のようにboot2dockerが起動されていることを確認できます。

![VirtualBoxコンソール]({{site.baseurl}}/images/boot2docker_virtualbox.png)

あとは普通にdockerコマンドを使用することができます。実際にDockerは仮想マシン上で実行されているのですが、それを意識する必要はありません。

以下のコマンドでboot2dockerを終了することができます。

```bash
$ boot2docker halt
```

ちなみにVagrantも1.6でDockerをサポートしていますが、やはり同じようにDocker自体は仮想マシン上での動作になります。また、Windowsではプロバイダにdockerを指定する場合、Cygwinを入れておかないと（rsyncが必要っぽい）起動できないという問題があるようです。

VagrantfileにDockerfileを指定しておくとVMの起動と同時にコンテナを起動できたりするようですが、ホスト側から直接dockerコマンドを叩いたりはできないようなので、MacでDockerを使うのであればboot2dockerが手軽でよいのではないかと思います。