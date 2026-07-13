# Tsundoku

## サービス名

Tsundoku
※積読とは違い、読んでいった本を積むことをTsundokuと定義しています。

## サービスURL

https://tsundoku.tech

## サービス概要
Tsundokuは「読書はしたいけれど、つい先延ばしにしてしまう」「読書習慣がなかなか続かない」といった問題を解決するための読書管理アプリです。
章ごとにメモを取り、読書ログをつけることで、自分の読書履歴を簡単に記録できます。また、GitHubのContributionグラフのように読書活動を視覚的に確認できるため、モチベーション維持につながります。

直近のリリース内容は[CHANGELOG.md](./CHANGELOG.md)を参照してください。

### 使用方法
| 本を検索 | 読書メモを取る | 読書ログを公開 |
| ---- | ---- |  ---- |
| 本を検索して、登録します。 | 本ごとにメモを取り、読書ログをつけます。 | 読書した本やログは公開できます。 |
| [![Image from Gyazo](https://i.gyazo.com/1a17a29e784994d7703c24620eca2d54.gif)](https://gyazo.com/1a17a29e784994d7703c24620eca2d54)| [![Image from Gyazo](https://i.gyazo.com/238d80b466672ff5a87e0cbae4f5a7a6.gif)](https://gyazo.com/238d80b466672ff5a87e0cbae4f5a7a6)| [![Image from Gyazo](https://i.gyazo.com/3c0ed8f17b3d992d5cfb00bd780dcd9a.jpg)](https://gyazo.com/3c0ed8f17b3d992d5cfb00bd780dcd9a) |


## 使用技術

### フロントエンド

![Next.js](https://img.shields.io/badge/Next.js-14.2.3-696969.svg?logo=nextdotjs)
![React](https://img.shields.io/badge/React-18-696969.svg?logo=react)
![Typescript](https://img.shields.io/badge/Typescript-5-696969.svg?logo=typescript)
![Storybook](https://img.shields.io/badge/Storybook-8.1.9-696969.svg?logo=storybook)
![Mantine](https://img.shields.io/badge/Mantine-7.12.2-696969.svg?logo=mantine)
![Auth.js](https://img.shields.io/badge/Auth.js-5.0.0--beta-696969.svg?logo=)

- Next.js(App Router) 14.2.3
- React 18
- TypeScript 5
- Mantine 7.12.2
- Storybook 8.1.9（UIカタログ / テスト）
- Auth.js(next-auth) 5.0.0-beta.18
- SWR 2.2.5（データフェッチ）
- Tiptap 2.4.0（リッチテキストエディタ）
- MSW 2.4.4（APIモック）

### バックエンド

![Rails](https://img.shields.io/badge/RubyonRails-8.0.5-696969.svg?logo=rubyonrails)
![Ruby](https://img.shields.io/badge/Ruby-4.0.5-696969.svg?logo=ruby)
![Rubocop](https://img.shields.io/badge/Rubocop-1.66.1-696969.svg?logo=rubocop)
![Rspec](https://img.shields.io/badge/Rspec-3.13.1-696969.svg?logo=rspec)
![Postgresql](https://img.shields.io/badge/PostgreSQL-696969.svg?logo=postgresql)
![Factorybot](https://img.shields.io/badge/Factorybot-6.5.0-696969.svg?logo=)
![Simplecov](https://img.shields.io/badge/Simplecov-0.22.0-696969.svg?logo=)

- Ruby on Rails 8.0.5
- Ruby 4.0.5
- PostgreSQL（`pg`gem 1.5.8）
- RuboCop 1.66.1 / rubocop-rails 2.26.2 / rubocop-performance 1.22.1
- RSpec 3.13.1 / FactoryBot 6.5.0 / SimpleCov 0.22.0
- Alba 3.2.0（JSONシリアライザ）
- Prosopite 2.2.0（N+1検知）
- Brakeman 8.0.4 / bundler-audit 0.9.3（セキュリティ静的解析）

## 起動方法

### インストール

`git clone --recurse-submodules https://github.com/reckyy/tsundoku.git`

### 起動の前準備

[Auth.js](https://authjs.dev/)を用いて認証機能を実装しています。
TsundokuではGoogleログインを採用しているため、起動前に以下の設定が必要です。
[Google OAuthの設定](https://github.com/reckyy/tsundoku/wiki/Google-OAuth%E3%81%AE%E8%A8%AD%E5%AE%9A)

また、本の検索には[楽天ブックス書籍検索API](https://webservice.rakuten.co.jp/documentation/books-book-search)を利用しています。[Rakuten Developers](https://webservice.rakuten.co.jp/)でアプリIDを発行し、後述の環境変数に設定してください。

### 環境変数の登録

`tsundoku-frontend/.env.local`を作成し、以下の内容を追加してください。
`AUTH_SECRET`は`npx auth secret`で生成された値を入力します。

```
AUTH_GOOGLE_ID={CLIENT_ID}
AUTH_GOOGLE_SECRET={CLIENT_SECRET}
AUTH_SECRET={YOUR_SECRET}
NEXT_PUBLIC_RAILS_API_URL="http://localhost:3001/api"
RAILS_API_URL="http://localhost:3001/api"
NEXT_PUBLIC_NEXT_URL="http://localhost:3000"
STORYBOOK_NEXT_PUBLIC_RAILS_API_URL="http://localhost:3001/api"
RAKUTEN_API_APPLICATION_ID={RAKUTEN_APP_ID}
RAKUTEN_API_ACCESS_KEY={RAKUTEN_ACCESS_KEY}
```

続いて、`.tsundoku-backend/.env`を作成し、以下の内容を追加してください。
`SECRET_KEY_BASE`は`openssl rand -hex 64`などで生成したランダムな値を設定します。
`AUDIENCE`にはGoogle OAuthのクライアントID（`AUTH_GOOGLE_ID`と同じ値）を設定します。
```
SECRET_KEY_BASE={YOUR_SECRET_KEY_BASE}
AUDIENCE={CLIENT_ID}
ISSUER='https://accounts.google.com'
```

### セットアップ

`bin/setup`

### 起動

`bin/dev`

## テスト

### バックエンドのテスト

```
cd tsundoku-backend
bundle exec rspec
bundle exec rubocop
bundle exec brakeman
bundle exec bundle-audit check --update
```

### フロントエンドのテスト

```
cd tsundoku-frontend
npm run storybook
# 上記を実行したターミナルは開いたまま、別のターミナルで以下を実行
npm run test-storybook
# 実行結果をブラウザで見たい場合は
open coverage/storybook/lcov-report/index.html
```
