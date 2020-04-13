# テストを体験してみる

本資料は、
https://github.com/thinkitcojp/RancherBook-samples
をフォークしたものです。

ベースとしては、
[RancherによるKubernetes活用完全ガイド ThinkIT Books](https://www.amazon.co.jp/dp/B07VCRBSRW)
のサンプルコードを改修したものになります。

## 前提環境

本リポジトリは以下の環境で動作確認をしています。

+ docker desktop 2.2.0.5 (for macOS)
  + docker-ce 19.03.8
+ docker-compose 1.25.4

## アプリケーションの内容

タスク管理のAPIを備えたサーバサイドアプリケーション(`server`ディレクトリ配下)、
それにアクセスするためのCLIアプリケーション(`client`ディレクトリ配下)を作成しています。

### サーバサイドアプリケーション

[Django](https://www.djangoproject.com/)および、[Django REST framework](https://www.django-rest-framework.org/)を
使ったタスク管理アプリケーションです。

### クライアントサイドアプリケーション

[cobra](https://github.com/spf13/cobra)を使って作成したCLIアプリケーションです。
サーバサイドアプリケーションにアクセスするためのクライアントを準備しています。

## 実行方法

基本的には、docker-composeを使って実行することを前提としています。
サーバサイドのテストを実行する際は以下のような手順で実行します。

```console
$ docker-compose up --build --abort-on-container-exit --exit-code-from todo-client

WARNING: The TODO_TESTSERVER variable is not set. Defaulting to a blank string.
Building todo-client
Step 1/5 : FROM golang:1.11 as builder
 ---> 43a154fee764
〜〜省略〜〜
todo-client_1  | 21     updated RUNNING updated description
todo-client_1  | 2020/04/13 09:57:34 Task(ID=21) is updated.
todo-client_1  | 2020/04/13 09:57:34 Task(ID=21) is updated.
rancherbook-samples_todo-client_1 exited with code 0
Aborting on container exit...
Stopping rancherbook-samples_todo-mysql_1  ... done
Stopping rancherbook-samples_todo-server_1 ... done
```
