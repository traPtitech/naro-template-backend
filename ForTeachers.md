# 講師向け資料

このMDはDockerのUbuntuイメージを用いて手元でまっさらな環境を準備するための資料です。実演のために受講者と同様の環境を準備することを想定しています。

## 必要な環境

- VSCode
  - 拡張機能 「[Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)」
- Docker Desktop

## 作業

以下の内容のDockerfileを用意する。

```Dockerfile
FROM ubuntu:latest
```

### Ubuntuイメージの準備

```bash
docker pull ubuntu:latest
docker run -it -d ubuntu
docker container ls #起動中のコンテナの名前を確認
```

```txt
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS          PORTS     NAMES
f42ed9e458a9   ubuntu    "/bin/bash"   50 seconds ago   Up 48 seconds             amazing_hypatia
```

今回であればコンテナ名は`amazing_hypatia`

```bash
docker exec -it {コンテナ名} bash
```

これでコンテナで動いているUbuntuに入ることができる。`exit`で抜けられる。これ以降は特に何も書いてない限りはUbuntuコンテナの中で操作する。

### Ubuntuの環境準備

```bash
apt update
apt upgrade
```

この状態だとUbuntuにはほとんど何も入っていない。

まずはユーザーを作る。

```bash
adduser {ユーザー名}
```

パスワードを2回入力し、それ以降の`Enter the new value, or press ENTER for the default`は全てEnterを押す。

sudoグループに新しく作ったユーザーを追加するために、sudoをインストールする。

```bash
apt install sudo -y
sudo gpasswd -a {ユーザー名} sudo
```

新しく作ったユーザーでログインする。パスワードが必要。

```bash
su - {ユーザー名}
pwd
```

```txt
/home/{ユーザー名}
```

ホームディレクトリに移動できる。

基本的なコマンドをインストールしておく。

```bash
sudo apt install wget -y
```

## 参考

https://www-creators.com/archives/241
https://e-penguiner.com/vscode-developent-environment-docker-without-root/
https://bearmini.hatenablog.com/entry/2014/05/14/130148
https://docs.docker.jp/engine/reference/builder.html#
