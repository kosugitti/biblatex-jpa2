# biblatex-jpa2

日本心理学会『執筆・投稿の手びき』（2022年版）に準拠した BibLaTeX スタイルファイルです。

[biblatex-jpa](https://github.com/sbtseiji/biblatex-jpa)（芝田征司氏作成）を参考に、言語切替の設計をゼロから再構築しています。

## 特徴

- **`langid` フィールドによる自動言語切替** — エントリごとに日本語/英語のフォーマットを自動適用
- **`language = {japanese}` との後方互換** — biber の sourcemap で `langid` に自動変換
- **言語設定の一元管理** — `\jpa@setJapanese` / `\jpa@setEnglish` に集約
- **マニュアル見本 3.8 / セクション 3.10 の全パターンをテスト収録**

## ファイル構成

```
biblatex/
├── jpa2.bbx          ドライバ定義（文献リスト）
├── jpa2.cbx          引用スタイル
├── jpa2.dbx          カスタムデータモデル
├── english-jpa2.lbx  英語設定（将来の autolang 対応用）
└── japanese-jpa2.lbx 日本語設定（将来の autolang 対応用）
doc/
├── jpa2-manual.tex   テスト文書
└── sample.bib        マニュアル見本の全引用例
```

## 使い方

### スタイルファイルの設置

`biblatex/` 内の 5 ファイル（`.bbx`, `.cbx`, `.dbx`, `.lbx` x2）を TeX の検索パスに配置してください。

### プリアンブル

```latex
\documentclass[a4paper]{jlreq}
\usepackage[backend=biber, style=jpa2]{biblatex}
\addbibresource{文献.bib}
```

### bib ファイルの書き方

日本語文献には `langid = {japanese}` を指定してください。

```bibtex
@article{Fukaya2011,
  author       = {深谷, 達史},
  sortname     = {Fukaya, Tatsushi},
  sorttitle    = {かがくてきがいねんのがくしゅうにおける},
  date         = {2011},
  title        = {科学的概念の学習における自己説明プロンプトの効果},
  subtitle     = {SBF理論に基づく介入},
  journaltitle = {認知科学},
  volume       = {18},
  pages        = {190--201},
  doi          = {10.11225/jcss.18.190},
  langid       = {japanese},
}
```

英語文献には `langid` の指定は不要です（デフォルトで英語として処理されます）。

既存の bib ファイルで `language = {japanese}` を使用している場合も、自動的に `langid` に変換されます。

### 日本語文献のソートに関する注意

日本語文献の正しいソート順（五十音順）を保証するために、以下のフィールドを指定してください。

- **`sortname`**: 著者名のローマ字表記（例: `Fukaya, Tatsushi`）
- **`sorttitle`**: タイトルのひらがな読み（例: `かがくてきがいねん...`）

`sorttitle` は同一著者・同一年の文献が複数ある場合の extradate（a, b, ...）の割り当てに影響します。ひらがなで指定することで、biber が Unicode の五十音順（か < が < き < ぎ ...）で正しくソートします。

### 文献リストの出力

```latex
\printbibliography[title=引用文献]
```

## 対応エントリタイプ

| エントリタイプ | 用途 |
|------------|------|
| `@article` | 雑誌論文、紀要、Advance online publication |
| `@book` | 書籍（一般、版数、編集書、翻訳書） |
| `@inbook` | 編集書中の特定章 |
| `@mvbook` | 数巻にわたる書籍 |
| `@incollection` | シリーズの特定の1巻 |
| `@online` | プレプリント、ウェブ資料 |
| `@thesis` | 学位論文 |
| `@inproceedings` | 学会発表 |
| `@report` | 年報・年鑑 |
| `@misc` | 新聞・雑誌記事 |
| `@software` | ソフトウェア |

## 注意事項

- このスタイルファイルは個人が作成したものであり、日本心理学会によるものではありません
- LuaLaTeX + jlreq での使用を推奨します
- biblatex 3.17 以降 + biber 2.17 以降が必要です

## ライセンス

LPPL (LaTeX Project Public License)

## 謝辞

- [biblatex-jpa](https://github.com/sbtseiji/biblatex-jpa)（芝田征司氏） — 設計の参考元
- 日本心理学会『執筆・投稿の手びき（2022年版）』 — フォーマット仕様
