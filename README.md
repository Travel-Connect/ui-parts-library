# PARTS — UIパーツライブラリ

見た目と名前からUIを探すライブラリです。8種類の辞書項目に、公式サイトから収集した16件の実例と8件の表示画像をひも付けています。

[公開サイト](https://ui-parts-atlas-20260915.travelconnect.chatgpt.site) · [GitHub](https://github.com/Travel-Connect/ui-parts-library)

## 開く

`dist/index.html` をブラウザーで開くか、`python -m http.server 4381 --bind 127.0.0.1 --directory dist` でローカル表示できます。ビルドや依存パッケージのインストールは不要です。

## 検討できる操作

- 見た目を主役にしたカード一覧／説明を読みやすいリスト一覧
- 名前、別名、用途による検索とカテゴリ絞り込み
- 詳細パネルで公式実例、出典、確認日、取得画像を見る
- 独自の動作サンプルで8種類の部品を試す
- 気になる部品のお気に入りと個別メモ

## 範囲

Modal dialog、Drawer、Popover、Command palette、Data table、Tabs、Toast、Date range picker を収録しています。公式実例はRadix Primitives、shadcn/ui、Ant Design、React Aria、GitHubの公開資料から収集し、日本語の説明は独自に要約しています。

一覧の画像は公式ページの対象部品を取得したものです。「動作サンプル」タブはこのライブラリ独自のデモです。取得画像には確認元URL・取得日時・表示状態・ハッシュ値を保存しています。画像がない実例は出典ページと説明で表示します。

収集データはGitで管理するJSONです。お気に入り・メモ・表示形式は各ブラウザー内に保存し、公開リポジトリやサイトの共有データへ送信しません。端末間同期、サーバーDB、画像登録画面、100項目全体の辞書は今回の範囲に含みません。各動作デモの変更はデモ内だけに反映されます。Drawerデモはノンモーダル、一覧の詳細パネルはモーダルです。

JavaScriptが有効な現行ブラウザーを想定します。外部フォントが読み込めない場合はシステムフォントを使用します。WebMCP対応ブラウザーでは検索・詳細表示の2操作を登録します。

## 構成

- `dist/index.html`: 一覧ページの構造
- `dist/styles.css`: レイアウト、各部品の縮小プレビュー、レスポンシブ表示
- `dist/app.js`: 検索、実例表示、詳細、8種類の独立した動作デモ
- `dist/data/catalog.json`: 辞書と公式実例の収集データ（編集元）
- `dist/data/catalog.js`: JSONから生成するブラウザー用データ
- `dist/assets/examples/`: 出典と対応付けた公式UIの取得画像
- `scripts/build-catalog.mjs`: データの関係・URL・画像ハッシュの検証と生成
- `.openai/hosting.json`: Sitesのホスティング設定

## データを追加する

`dist/data/catalog.json` の `parts` と `examples` を編集し、次を実行します。

```sh
node scripts/build-catalog.mjs
node --check dist/app.js
```

生成結果が編集元と一致しているかは `node scripts/build-catalog.mjs --check` で確認できます。[収集ルール](docs/collection.md)に記録項目と確認範囲をまとめています。

## 検証

2026-09-15: 独立したjsdom環境で検索・表示切替・お気に入り・メモ・実例表示・文字列のエスケープ、および8種のデモの主要操作を36項目確認し、すべて成功しました。収集データの参照関係、画像ハッシュ、JavaScript構文を検証しています。

公式サイトでは代表例8件の表示画像を取得しました。このうち5件は開く操作またはタブ切替の範囲を確認し、それ以外の操作・アクセシビリティは未検証です。Date range pickerの画像は開始・終了の入力欄を閉じた状態で取得しています。GitHub Command Paletteは製品の操作資料として収録し、掲載ページ内のライブデモとは扱いません。

ライブラリ自体の実ブラウザーE2E、フォーカス制御、画面幅ごとの見た目は未検証です。WebMCPは対応する実ブラウザーの検証環境が利用できず、登録・呼び出しを未検証として残しています。
