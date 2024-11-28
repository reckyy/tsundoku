# Tsundoku

## サービス名

Tsundoku
※積読とは違い、読んでいった本を積むことをTsundokuと定義しています。

## サービスURL

https://tsundoku.tech

## サービス概要

Tsundokuは「読書はしたいけれど、つい先延ばしにしてしまう」「読書習慣がなかなか続かない」といった問題を解決するための読書管理アプリです。  
ユーザーは、読む本を登録し、章ごとにメモを取ることで読書ログをつけることができます。メモを取った日は自動的にログが記録され、読んだ本の一覧表示や、GitHubのContributionグラフのように視覚的に読書習慣を確認できます。また、読書ログを外部に公開してアピールすることも可能で、これにより読書習慣の維持と促進が期待できます。

### 使用方法
| 本を検索 | 読書メモを取る | 読書ログを公開 |
| ---- | ---- |  ---- |
| 本を検索して、登録します。 | 本ごとにメモを取り、読書ログをつけます。 | 読書した本やログは公開できます。 |
| [![Image from Gyazo](https://i.gyazo.com/1c47d9f16c328a7f9908ba4de1492b40.gif)](https://gyazo.com/1c47d9f16c328a7f9908ba4de1492b40) | [![Image from Gyazo](https://i.gyazo.com/723d9ab170b2dd555b133614bd4c08c9.gif)](https://gyazo.com/723d9ab170b2dd555b133614bd4c08c9) | [![Image from Gyazo](https://i.gyazo.com/4729da63da9649d1a6c027a7a690c81c.jpg)](https://gyazo.com/4729da63da9649d1a6c027a7a690c81c) |


## 使用技術

### フロントエンド

![Next.js](https://img.shields.io/badge/Next.js-696969.svg?logo=nextdotjs)
![React](https://img.shields.io/badge/React-696969.svg?logo=react)
![Typescript](https://img.shields.io/badge/Typescript-696969.svg?logo=typescript)
![Storybook](https://img.shields.io/badge/Storybook-696969.svg?logo=storybook)
![Mantine](https://img.shields.io/badge/Mantine-696969.svg?logo=mantine)
![Auth.js](https://img.shields.io/badge/Auth.js-696969.svg?logo=)

- Next.js App Router 14.2.3
- React 18
- TypeScript 5
- Storybook 8.1.9
- Mantine 7.12.2
- Auth.js 5.0.0

### バックエンド

![Rails](https://img.shields.io/badge/RubyonRails-696969.svg?logo=rubyonrails)
![Ruby](https://img.shields.io/badge/Ruby-3.3.1-696969.svg?logo=ruby)
![Rubocop](https://img.shields.io/badge/Rubocop-1.64.0-696969.svg?logo=rubocop)
![Rspec](https://img.shields.io/badge/Rspec-3.13.0-696969.svg?logo=rspec)
![Postgresql](https://img.shields.io/badge/Postgresql-1.5.6-696969.svg?logo=postgresql)
![Factorybot](https://img.shields.io/badge/Factorybot-6.4.6-696969.svg?logo=)
![Simplecov](https://img.shields.io/badge/Simplecov-0.22.0-696969.svg?logo=)

- Ruby on Rails7.2.1
- Ruby 3.3.5
- RuboCop 1.66.1
- RSpec 3.13.1
- PostgreSQL
- FactoryBot 6.5.0
- SimpleCov 0.22.0

## 起動方法

### インストール

`git clone --recurse-submodules https://github.com/reckyy/tsundoku.git`

### 起動の前準備

今回[Auth.js](https://authjs.dev/)を用いて、認証機能を実装しています。
Tsundokuでは、Googleログインを採用しているため起動前に以下の設定をする必要があります。
[Google OAuthの設定](https://github.com/reckyy/tsundoku/wiki/Google-OAuth%E3%81%AE%E8%A8%AD%E5%AE%9A)

### 環境変数の登録

`.env.local`を作成し、以下の内容を追加してください。
`AUTH_SECRET`は、`npx auth secret`で生成された値を入力してください。

```
AUTH_GOOGLE_ID={CLIENT_ID}
AUTH_GOOGLE_SECRET={CLIENT_SECRET}
AUTH_SECRET={YOUR_SECRET}
NEXT_PUBLIC_RAILS_API_URL="http://localhost:3001/api"
NEXT_PUBLIC_NEXT_URL="http://localhost:3000"
STORYBOOK_NEXT_PUBLIC_RAILS_API_URL="http://localhost:3001/api"
STORYBOOK_NEXT_PUBLIC_NEXT_URL="http://localhost:3000"
```

### セットアップ

`bin/setup`

### 起動

`bin/dev`

## テスト

### バックエンドのテスト

```ruby
cd tsundoku-backend
rspec
rubocop
```

### フロントエンドのテスト

```typescript
cd tsundoku-frontend
npm run storybook
// 上記を実行したターミナルは開いたまま別のターミナルで下のコードを実行
npm run test-storybook
// 実行結果をブラウザで見たい場合は
open coverage/storybook/lcov-report/index.html
```
