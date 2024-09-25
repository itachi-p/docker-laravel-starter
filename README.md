# Laravel Docker Starter

（基本的に自分用備忘録）
このリポジトリは、PHP、Laravel、MySQL環境をDockerを使用して簡単にセットアップするためのテンプレです。
以下の手順に従って、すぐにLaravelアプリケーション（開発環境）を動かすことができるようにします。
※手軽なスターターキットとしてLaravel Sailがあるが、学習目的で敢えて車輪の再開発を行うのが趣旨

## 前提条件
- Dockerインストール済み
- Docker Composeインストール済み

## セットアップ手順

1. リポジトリをクローン
    ```bash
    git clone https://github.com/yourusername/laravel-docker-starter.git
    cd laravel-docker-starter
    ```

2. 環境変数ファイルをコピー
    ```bash
    cp .env.example .env
    ```

3. Dockerコンテナをビルドして起動
    ```bash
    docker-compose up -d --build
    ```

4. **コンテナ内で**Laravelの依存関係をインストール
    ```bash
    docker-compose exec app composer install
    ```

5. アプリケーションキーを生成（Laravelアプリのセキュリティ上重要）
    ```bash
    docker-compose exec app php artisan key:generate
    ```

6. マイグレーションを実行（同じDB環境の準備）
    ```bash
    docker-compose exec app php artisan migrate
    ```
7. データベースのレコード（またはダミーデータ群）も再現する場合（シーディング）
    ```bash
    docker-compose exec app php artisan db:seed
    ```

## アクセス
- アプリケーション: http://localhost:8000
- phpMyAdmin: http://localhost:80/phpmyadmin5/
(MySQL自体はport:3306)

## デプロイ
このリポジトリをDockerHub、Google Cloud Run、AWSなどにデプロイする手順については、後日追加予定
