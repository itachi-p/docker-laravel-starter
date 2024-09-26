# Docker 学び直し(2024/09)

## 概要

- 過去何度かAWS、DockerHub、Heroku等にDockerイメージのデプロイはしたが、忘れている＆変わっているので学び直し
- 学習（記憶の定着）とは即ち反復である
- 写経や1回のハンズオンでやった気にはなれるが、人は忘れる

### 方針

**最小コストで**Dockerのきほんのキ゚を抑え、今後Laravelアプリ新規開発時の環境構築コストを下げる。

- 時間とは今回の人生の残り期間である
- 他に優先順位高い学習対象が多数あるので、現状ではDockerに対する理解は基本の範囲に留める（過剰なコストをかけない）
- コストとは学習コスト、主に時間と費用のこと。コストコとは関係ない。ところでコストが小さいからコストコなのか？
- このファイルも極力Vim（またはVSCodeのVim拡張機能キーバインド）で編集する
- Laravel Sailを使えば早いが、敢えて車輪の再開発で理解と応用力を深める
  - Laravel Sailも動作確認済み（事前のファイルシェアリングとポートの競合に注意）

2018年に購入した [Udemy教材](https://www.udemy.com/share/1026SG3@T3dICekDwtHbptE_TVrvXSQaJovioib1GIRo6Ig2nSCgBDQWWTzLJZyHwtI7__OK/) が消化率40%（約6.5時間）のまま~~だが、そちらは今回敢えて使わない。~~ だったが、今回これを消化する。(100%かどうかは未定）


### 重要用語

- Docker Image　（レシピ）
- Docker Container　（料理）
- Docker Repository
- Docker Compose　（コンテナの連携）
- Docker Volumes

Docker Image: 料理の元となる材料またはレシピのようなもの。アプリケーションやその依存関係、設定などを含む静的なテンプレート
Docker Container: レシピから作られる料理のようなもの。Docker Imageを*Dockerfile*の記述に従って実行したもので、実際の開発または実行環境そのもの
Docker Repository: GitHubのような、コンテナ（イメージ）のデプロイ先でありダウンロード元。Docker Hubなどが代表的
Docker Compose: 各コンテナの連携を司るツール。複数のコンテナを定義し、まとめて管理・実行するための設定ファイル（docker-compose.yml）を使用する
Docker Volumes: コンテナ間でデータを永続化・共有するための仕組み。コンテナが削除されてもデータが保持されるため、データベースなどの永続的なデータを扱う際に使用される

#### TIPS

- Docker Desctop: MacでもWindowsでも大幅に利便性が増す（ただしリソースを多く食うのでマシンパワー必須）
- Docker init: Dockerfileやdocker-compose.yaml(compose.yml)、.dockerignoreの雛形を自動生成できる
- Docker Compose Watch: コンテナを再三downする必要なく起動したままで変更が反映される(ホットリロード)
利用にはcompose.ymlに以下のような設定の追記が必要

```compose.yml
services:
  web:
    build: .
    command: npm start
    develop:
      watch:
        - action: sync
          path: ./web
          target: /usr/src/web
          ignore:
            - node_modules/
        - action: rebuild
          path: package.json

```

(Docker公式Compose Watch説明ページ)[https://docs.docker.com/compose/how-tos/file-watch/]

- Docker Scout: 脆弱性や依存関係のスキャン、セキュリティ強化
- Docker Build Cloud: クラウド上でイメージをローカル実行よりかなり高速にビルドできる環境
またチーム開発の際にもクラウド上で共有できるため、冗長なビルドが不要になり開発効率が増すメリットがある
ただしFleeプランの場合は、1アカウントにつき月に50分までの利用制限がある


