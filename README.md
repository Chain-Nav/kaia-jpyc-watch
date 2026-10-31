# Unifi・JPYC・Kaia ウォッチ

公開中のサイト：https://kaia-jpyc-desk.pages.dev

Unifi・JPYC・Kaia の価格・JPYC流通量・Unifiのリワード率・ニュースを、毎日追えるサイトです。
このリポジトリには、サイトのページと文章だけが入っています。

## 中身

| 場所 | 内容 |
|---|---|
| `kaia_site/public/index.html` | ページ本体。HTML・CSS・JavaScript が1ファイルに入っています |
| `kaia_site/public/knowledge.json` | 解説・用語・使い方・リスク・年表などの文章。下の2つのファイルから作ります |
| `kaia_knowledge.yaml` | 文章の元（解説カード・基本データ・年表・リンク・リスク・使い方・困ったとき・リワード率） |
| `kaia_glossary.yaml` | 用語の元 |
| `kaia_site/build.py` | 上の2つから `knowledge.json` を作る（`python kaia_site/build.py`。PyYAML が必要） |
| `kaia_site/public/`（そのほか） | アイコン・`manifest.webmanifest`（ホーム画面に追加用）・`_headers`・`robots.txt` |
| `kaia_site/functions/`・`schema.sql` | 閲覧数を数える仕組み（Cloudflare Pages Functions と D1）。見た目には関係ありません |

## データの出どころ

- **ニュース・数字・毎日の記録・利率の変更**：`https://raw.githubusercontent.com/sajicosaji/crypto-news-bot/kaia-data/kaia/site.json`（1時間おきに自動で更新）
- **ページがブラウザから直接取っているもの**
  - KAIAの価格：CoinGecko（混んでいるときは bitbank と DefiLlama）
  - JPYCの流通量：各チェーン（Ethereum・Polygon・Avalanche・Kaia）のRPC
  - Unifiのリワード率・お知らせ：api.unifi.me
  - Kaiaのブロック・ガス代：Kaiaの公開RPC
  - DeFiの預かり（TVL）など：DefiLlama

## 手元で見る

```
cd kaia_site/public
python -m http.server 8000
```

http://localhost:8000 を開きます。データは上のURLから取るので、手元でもいつもと同じ中身で表示されます。

## 作り直すときに残してほしいところ

- タブ（`home`・`news`・`guide`・`risk`・`market`・`learn`・`words`）と、URLの `#news` などでそのタブが開く動き
- `localStorage` の `watch.〜`（前回見た時刻をもとに、NEW の印やニュースの件数を出しています）
- 文章の中の `{{JPYC}}`・`{{USDT_BASIC}}`・`{{USDT_PLUS}}`・`{{USDT_MAX}}`・`{{JPYC_10K}}`（ページで公式の今の利率に置きかわります）
- `hit(…)` の呼び出し（閲覧数用）
- リスクの印は 😈。悪い話も良い話と同じ重さで見せる
- ページの下の注釈や「このページは〜」のような説明文は入れない
- 検索エンジンには出さない（`noindex`）

## 変更について

このリポジトリは見せる用の写しで、公開中のサイトへの反映は持ち主が行います。
変えたいときは fork して作業し、できたら知らせてください（Pull Request でも大丈夫です）。
