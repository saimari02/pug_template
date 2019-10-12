複数ページあるwebサイト用に、pugの構成を考えました。

# EditorConfig
`editorconfig`  
Pugはスペースとタブが混在するとエラーになってしまうのでEditorConfigを導入して解決しています。
EditorConfigはテキストエディタによって設定やパッケージがあるので準備しておいてください。

*参考：[EditorConfig でチームみんなのエディタの設定を揃える](https://www.tam-tam.co.jp/tipsnote/program/post6306.html)*

# ディレクトリ構成
```
pug root/
├ index.pug
├ 2nd/
│ └ index.pug
│ 　 └ 3rd/
│ 　 　 └ index.pug
│
├ assets/
│ └ include/
│ 　 ├ common_header.pug
│ 　 ├ common_footer.pug
│ 　 ├ gtm_body.pug
│ 　 └ gtm_head.pug
│
└ _include/
　 ├ _breadcrumb.pug
　 ├ _const.pug
　 ├ _inquiry.pug
　 ├ _layout.pug
　 ├ _link.pug
　 ├ _meta.pug
　 ├ _script.pug
　 └ _sns-share.pug
```
※第3階層まであるサイトのディレクトリ構成を想定としています。

## コンパイルされるファイル
```
assets/include/~
```
- `common_header` => 共通ヘッダー
- `common_footer` =>共通フッター
- `gtm_body` => Google Tag Managerのscript記述
- `gtm_head` => Google Tag Managerのscript記述

コンパイル時、ファイルとして書き出されます。<br>
各htmlファイル内で `<?php include>`で読み込まれるよう仕様になっています。

## コンパイルされないファイル
```
_include/~
```
- _breadcrumb => パンくずリストのファイル
- _const => サイト全体の変数をまとめるファイル
- _inquiry => お問い合わせエリア（共通レイアウト）のファイル
- _layout => サイト全体の共通レイアウトファイル
- _link => `<head>`内の`<link>`の記述をまとめるファイル
- _meta => `<head>`内の`<meta>`の記述をまとめるファイル
- _script => `<head>`内の`<script>`の記述をまとめるファイル（※要defer属性をつける）
- _sns-share => SNSのシェアボタン（共通レイアウト）のファイル

# 各ファイル内の設定
|  変数 |  内容  |  入力値  |
| ---- | ---- | ---- |
| `pagePrefix` | `<head>`のpagePrefixと、`og:type`の設定。 | `website` or `article` |
| `searchIndex`| 検索ロボットにクロールさせるか否か。 | `true` or `false` |
| `pageDirectory` | ページの階層 | `1st` or `2nd` or `3rd` |
| `pageSlag` | 現在のページのURLのslag | Stringで入力 |
| `directory02Slag` | 第二階層のURLのslag<br>**※第三階層のみ入力** | Stringで入力 |
| `pageTitle` | 現在のページのタイトル | 日本語で入力 |
| `directory02Title` | 第二階層のタイトル<br>**※第三階層のみ入力** | 日本語で入力 |
| `pageDescription` | 現在のページのdescription |	日本語で入力 |
| `contactURL` | お問い合わせ先のURLのパス | URLを入力 |

# 補足
※コンパイル環境設定に関してはこちらに記載しておりません。<br>webpackや、gulpなどでコンパイルしてください。

# 参考
- [Pugドキュメント翻訳](https://tr.you84815.space/pug/)
- [これからのコーディングは再利用と効率化だ！話題のPugを使ってみた](https://cultureacademia.jp/webcreate/312/)