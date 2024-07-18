---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Welcome to Slidev
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# https://sli.dev/guide/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/guide/syntax#mdc-syntax
mdc: true
---

# S3バケットをtreeしたい！

2024/07/17 @AWS Likers

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: fade-out
---

# LTの趣旨

OSS(創作)活動はイイぞという話とツールの紹介

## 効能
- 📝 とりあえず手を動かしてOSS公開することで思わぬ学びがあったりする
- 🎨 一見くだらなそうでもやり切ることが大事
- 🧑‍💻 OSSを通じた交流活動？

<br>
<br>

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<!--
Here is another comment.
-->

---
transition: slide-up
level: 2
dragPos:
  square: 622,136,230,230
---

# 自己紹介

## Takafumi Miyanaga

### 職業
- バックエンド〜フロントエンドエンジニア

### 趣味
- 暇を見つけてちょっと便利なツールを作ること

### 各種アカウント
@orangekame3 - GitHub, Twitter

<img v-drag="'square'" src="/orangekame3.jpg">

---
dragPos:
  square: 14,391,226,114
  tftarget: 22,381,204,103
  paclear: 240,374,234,117
  ghfetch: 502,364,206,130
  mk: 742,366,188,125
---

# これまで作ったもの

- **[tftarget](https://github.com/future-architect/tftarget)** - Terraformのtargetオプションを使いやすくするツール
- **[paclear](https://github.com/orangekame3/paclear)** - `clear`のジョークコマンド
- **[ghfetch](https://github.com/orangekame3/ghfetch)** - GitHubのAPIを叩いて`neofetch`ライクに情報を表示するツール
- **[mk](https://github.com/orangekame3/mk)** - Makfieleベースのインタラクティブタスクランナー
- **[stree](https://github.com/orangekame3/stree)**　- S3バケットをtreeしたい！←ほんじつのテーマ

<img v-drag="'tftarget'" src="/tftarget.gif">
<img v-drag="'paclear'" src="/paclear.gif">
<img v-drag="'ghfetch'" src="/ghfetch.gif">
<img v-drag="'mk'" src="/mk.gif">

---
layout: cover
---

# モチベーション

---
layout: center
---

# 皆さんはこんなこと思ったことないでしょうか？

---
layout: center

---

# aws cliコマンドには`ls`コマンドや`cp`コマンドがあるのに`tree`コマンドはないの？

---
layout: center

---

# そもそもAWSのS3バケットにフォルダのような階層構造ってあったっけ？

---
layout: two-cols-header
---
# タイムリーな記事を先週見かけました

::left::

<Tweet scale=0.6 id="1810473460264775928" />

::right::

## 記事の内容
- Amazon S3にはフォルダのような階層構造はない
- S3はオブジェクトストレージであるため、フォルダは単なるプレフィックス
- フォルダのように見えるのはS3コンソールやAWS CLIがプレフィックスを使って表示しているため

## 補足
- S3にフォルダを作成しようとすると0バイトのオブジェクトが生成される
- これがフォルダのように見える

---
layout: center

---

# なるほど

---
layout: center

---

# フォルダ構造はないが、擬似的にtree表示することはできそうだ

---
layout: center

---

# 同志をさがす

---
layout: iframe-right

<!-- url: https://dev.classmethod.jp/articles/s3-tree-aws-s3-ls/ -->

class: my-cool-content-on-the-right
---

# いました

さすがクラスメソッドさんです

以下のコマンドでインストール

```bash
pip install s3-tree
```

以下のような出力が得られるようです。

```bash
s3-tree awsliker-0717
awsliker-0717
└── 2023
    ├── 12
    │   ├── 28
    │   │   └── dummy.txt
    │   ├── 29
    │   │   └── dummy.txt
    │   ├── 30
    │   │   └── dummy.txt
    │   └── 31
    │       └── dummy.txt
    └── heavy.txt

7 directories, 5 files

```


---
layout: center

---

# めでたしめでたし

---
layout: center

---

# とはなりませんでした


---

このツール、使ってみるといくつかの点で不満がありました

- 不満1
  - `profile`指定ができない
    - マルチアカウントを常用しているため、`profile`指定ができないと使いにくい
- 不満2
  - 特定の階層を指定してtree表示することができない
    - バケット全体の`tree`ではなく、特定の階層以下の情報を表示したいケースに対応できない
- 不満3
  - Python製のツールをグローバルにインストールするのはちょっと抵抗がある
    - `homebrew`やシングルバイナリで提供されていると使いやすい(宗教上の理由)
- 不満4
  - なんかもっさりしている？

---
---

# 簡単にベンチマークを取ってみました

気の所為ではなく、aws cliと比較してもっさりしていることがわかりました（2倍近い）

```bash
hyperfine --warmup 3 \
  'aws s3 ls awsliker-0717 --profile orangekame3' \
  's3-tree awsliker-0717' \
  --export-markdown benchmark_results.md
```

| Command                                         |     Mean [ms] | Min [ms] | Max [ms] |    Relative |
| :---------------------------------------------- | ------------: | -------: | -------: | ----------: |
| `aws s3 ls awsliker-0717 --profile orangekame3` |  417.2 ± 15.8 |    394.2 |    447.5 | 2.09 ± 0.18 |
| `s3-tree awsliker-0717`              | 922.0 ± 105.9 |    754.7 |   1177.5 | 4.62 ± 0.64 |


---
---

ということで先ほどの不満を解消するCLIツールを作りたいモチベーションになりました

- `profile`指定ができる
- 特定の階層を指定してtree表示することができる
- シングルバイナリで提供されている
- もっさりしていない


---
---

# 当時の心境

この時点での私の心境はざっと以下の通り

- そんなに必要ではないが、あると少し便利そうなツールかも？
- `list-object`で処理できる範囲で作りたい
- `tree`出力の部分は骨が折れそう(できれば既存のOSSに乗っかりたい)


---
---

# list-object-vでどこまでできる？

`aws s3api list-object-v2`で取得できる情報は以下の通り

- 以下の情報が取得可能
  - Key
  - LastModified
  - Size
  - Owner

```bash
aws s3api list-objects-v2 --bucket awsliker-0717 --profile orangekame3 --fetch-owner
{
    "Contents": [
        {
            "Key": "2023/12/28/dummy.txt",
            "LastModified": "2024-07-17T05:53:00+00:00",
            "Size": 0,
            ...
            "Owner": {
                "DisplayName": "orangekame3",
                "ID": "xxxxxxxxxxxxxxxxxxxxxxx"
            }
        },
        ...
}
```

---
layout: center

---

# list-object-v2でかなりの情報を取得できることを確認`tree`コマンドの既存のオプションをかなり模倣できそうな予感がしてきました。

---
layout: center

---

# `tree`の出力部分の実装はどうする？

---
layout: two-cols-header

---
# 既存OSSに乗っかることにしました

::left::

<Tweet scale=0.6 id="1418484057831133188" />

::right::

## gtreeの特徴
- CLIでの利用、Goライブラリとしての利用どちらも可能
- `root` と `node`を渡すことで`tree`表示が可能なシンプル設計
- 作者が日本人なので日本語記事が豊富！(大事)


---
layout: center

---

# さて、材料は揃ったので作りました

---
layout: center

---

# 作ったもの

---
layout: two-cols-header
dragPos:
  stree-logo: 540,111,349,349
  stree: 49,311,387,221
---

# stree
stree (S3 tree  => s three => stree)

https://github.com/orangekame3/stree


当初課題に上げていた以下の不満点は対応
- profile対応
- prefix対応
- Go製(シングルバイナリ brew経由でinstall可能)

<img v-drag="'stree-logo'" src="/stree.png"/>
<img v-drag="'stree'" src="/stree.gif"/>

---
---

# 実行速度

```bash
hyperfine --warmup 3 \
  'aws s3 ls awsliker-0717 --profile orangekame3' \
  's3-tree awsliker-0717' \
  'stree awsliker-0717 -p orangekame3' \
  --export-markdown benchmark_results.md
```

| Command                                         |     Mean [ms] | Min [ms] | Max [ms] |    Relative |
| :---------------------------------------------- | ------------: | -------: | -------: | ----------: |
| `aws s3 ls awsliker-0717 --profile orangekame3` |  417.2 ± 15.8 |    394.2 |    447.5 | 2.09 ± 0.18 |
| `s3-tree awsliker-0717`              | 922.0 ± 105.9 |    754.7 |   1177.5 | 4.62 ± 0.64 |
| `stree awsliker-0717 -p orangekame3`            |  199.5 ± 15.7 |    166.7 |    226.1 |        1.00 |

**aws s3 cliよりも2倍以上速く、s3-treeよりも4倍以上速い！**

---
---

# オプション一覧

```bash
Usage:
  stree [bucket/prefix] [flags]

Flags:
  -D, --date-time                Print the last modified time of each file.
  -d, --directory-only           List directories only.
  -e, --endpoint-url string      AWS endpoint URL to use (useful for local testing with LocalStack)
  -f, --full-path                Print the full path prefix for each file.
  -h, --help                     help for stree
  -H, --human-readable           Print the size of each file but in a more human readable way, e.g. appending a size letter for kilobytes (K), megabytes (M), gigabytes (G), terabytes (T), petabytes (P) and exabytes(E).
  -I, --inverse-pattern string   List files that do not match the pattern.
  -L, --level int                Descend only level directories
  -l, --local                    Use LocalStack configuration
  -m, --mfa                      Use Multi-Factor Authentication
  -n, --no-color                 Disable colorized output
  -o, --output string            Send output to filename.
  -P, --pattern string           List files that match the pattern.
  -p, --profile string           AWS profile to use (default "default")
  -r, --region string            AWS region to use (overrides the region specified in the profile)
  -s, --size                     Print the size of each file in bytes along with the name.
  -u, --username                 Print the owner of each file.
  -v, --version                  version for stree
```

---
layout: center
---

# いくつかのオプションを紹介

---
---

# `-D, --date-time`

最終更新時刻を表示

```bash
stree awsliker-0717 -p orangekame3 -D
awsliker-0717
└── 2023
    ├── 12
    │   ├── 28
    │   │   └── [Jul 17 14:53] dummy.txt
    │   ├── 29
    │   │   └── [Jul 17 14:53] dummy.txt
    │   ├── 30
    │   │   └── [Jul 17 14:53] dummy.txt
    │   └── 31
    │       └── [Jul 17 14:53] dummy.txt
    └── [Jul 17 14:53] heavy.txt

6 directories, 5 files
```

---
---

# `-f, --full-path`

フルパスを表示

```bash
stree awsliker-0717 -p orangekame3 -f
awsliker-0717
└── 2023
    ├── 12
    │   ├── 28
    │   │   └── awsliker-0717/2023/12/28/dummy.txt
    │   ├── 29
    │   │   └── awsliker-0717/2023/12/29/dummy.txt
    │   ├── 30
    │   │   └── awsliker-0717/2023/12/30/dummy.txt
    │   └── 31
    │       └── awsliker-0717/2023/12/31/dummy.txt
    └── awsliker-0717/2023/heavy.txt

6 directories, 5 files

```

---
---

# `-H, --human-readable`

ファイルサイズを人間が読みやすい形式で表示

```bash
stree awsliker-0717 -p orangekame3 -H
awsliker-0717
└── 2023
    ├── 12
    │   ├── 28
    │   │   └── [      0] dummy.txt
    │   ├── 29
    │   │   └── [      0] dummy.txt
    │   ├── 30
    │   │   └── [      0] dummy.txt
    │   └── 31
    │       └── [      0] dummy.txt
    └── [ 104.9M] heavy.txt

6 directories, 5 files
```

---
---

# `-L, --level`

指定した階層までのみ表示

```bash
stree awsliker-0717 -p orangekame3 -L 2
awsliker-0717
└── 2023
    ├── heavy.txt
    └── 12

2 directories, 1 files
```

---
dragPos:
  mfa-pr: 518,172,434,244
---

# `-m, --mfa`

MFAを使う

```bash
stree awsliker-0717 -p orangekame3 -m
```

https://github.com/orangekame3/stree/pull/25

<img v-drag="'mfa-pr'" src="/mfa-pr.png"/>

このMFAの実装はgtree作者の方にPRを頂きました


---
dragPos:
  fzf-stree: 56,744,980,265
---

# 応用編

例えばfzfを使って組み合わせれば`tree`ビューでファイルを選択しながらダウンロードすることができます。

```bash
stree-fzf-cp() {
  local args=("$@")
  local bucket="${args[0]}"
  shift
  local profile=""
  while (( "$#" )); do
    case "$1" in
      -p|--profile)
        profile=$2
        shift 2
        ;;
      -*)
        shift
        ;;
      *)
        break
        ;;
    esac
  done
  if [ -z "$profile" ]; then
    echo "Usage: stree <bucket/prefix> [flags] -p <profile>"
    return 1
  fi
  command stree "${args[@]}" -f | fzf-tmux -p 80% --reverse | awk -F '── ' '{print $2}' | xargs -I {} aws s3 cp s3://{} . --profile "$profile"
}
alias stree-fzf-cp=stree-fzf-cp
```

---
dragPos:
  article: 253,228,402,282
---

# コミュニティ系
以下の2記事で紹介がありました。

- [Community | AWS open source newsletter, #189](https://community.aws/content/2cXuki31b6cvPtkoOMdNNxfLKfr/aws-open-source-newsletter-189)
- [stree - A simple directory tree command for listing AWS S3 bucket](https://terminaltrove.com/stree/)

<img v-drag="'article'" src="/article.png"/>

---
---

# まとめ

OSS(創作)活動はイイぞという話

## 効能

- 📝 とりあえず手を動かしてOSS公開することで思わぬ学びがあったりする
- 🎨 一見くだらなそうでもやり切ることが大事
- 🧑‍💻 OSSを通じた交流活動？
