## [1.3.1] - 2026-07-26
### Fixed
- 本の並べ替え時に、移動元・移動先のstatusが一致しているか検証するように
- Memo本文をnullではなく空文字で初期化するように
- Editorの変更状態を分離し、保存成功時のみリセットするように修正
- API境界でユーザーIDの型を統一
- 脆弱性のある依存gem(loofah/rails-html-sanitizer)をCVE対応版へ更新

## [1.3.0] - 2026-07-12
### Added
- 未認証リダイレクト時にトーストで通知を表示
- APIエラー時に原因切り分け用のerrorボディを返却し、フロントでもstatus/bodyを保持するように

### Changed
- 本の並び順(acts_as_list)をステータスごとのスコープで管理するように
- フロントのAPI通信ロジックをclient/serverで共通化、PATCHリクエストの冗長なパラメータを削除
- RuboCopのTargetRubyVersionを実Ruby(4.0)に合わせ、新有効化されたcopの違反を修正
- READMEにバックエンドの環境変数(SECRET_KEY_BASE/AUDIENCE/ISSUER)の設定手順を追記

### Fixed
- Bookモデルにauthor/cover_image_urlのpresenceバリデーションを追加
- ユーザーページのURLコピー成否判定をコピー完了時に行うよう修正
- 脆弱性のある依存gem(nokogiri/concurrent-ruby/faraday/crass/websocket-driver)をCVE対応版へ更新

## [1.2.0] - 2026-06-16
### Added
- 想定外エラー時のフォールバック表示を追加
- CIにセキュリティスキャン（backend）とStorybook test-runner（frontend）を追加

### Changed
- backendのRubyを4.0.5へ更新（Heroku-26対応）、puma等の依存を更新
- フロントのAPI通信をaxiosからnative fetchへ全面移行
- ログイン時の本人識別をIDトークンのクレームに基づくよう変更（送信もIDトークンのみに）
- エラーハンドリング/セッション管理を集約・統一、本フィルタUIをSegmentedControlに整理、未使用dndライブラリを削除
- CORSを環境ごとに設定、非推奨の`:unprocessable_entity`を`:unprocessable_content`へ更新
- READMEを現行スタック・環境変数・テスト手順に更新

### Fixed
- N+1クエリを解消
- ボタンの二重送信を防止
- UserMenuの相対パス参照による404、middlewareのusers判定の正規表現を修正
- 未ログイン時のTopLoading表示、Headerの非null前提など複数の不具合を修正
- net-imapの脆弱性（CVE）に対応

## [1.1.4] - 2026-05-10
### Fixed
- 章タイトル/メモ保存の部分失敗が「成功」と表示され、サーバに未反映のまま後で巻き戻るデータロスを修正
- タブ切替復帰時に未保存のメモ入力が消える問題を修正
- 退会後のリダイレクト経路を統一

### Changed
- 本登録時の冗長なPOST呼び出しを除去し、ステータスコードを統一
- 本番環境向け`config.hosts`を設定
- 優先度lowおよびmedium1件（SWRデータ管理見直し）の修正・リファクタを取り込み

## [1.1.3] - 2026-04-19
### Fixed
- 優先度のhigh修正をリリースに取り込み
- 優先度mediumの修正を1つあわせて取り込み

## [1.1.2] - 2025-02-08
### Fixed
- 読書ログがない人がログインできない問題を修正。

## [1.1.1] - 2024-12-09
### Added
- 読書ログの年度切り替え機能を追加

### Fixed
- 読書ログが見切れていた問題を修正

## [1.0.1] - 2024-11-30
### Fixed
- 本登録時、必ず一度は登録失敗するバグを修正。
- 他の人の本が表示されてしまう問題を修正。
