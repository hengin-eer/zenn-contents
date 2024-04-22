---
title: "git addで謎の警告が気になるあなたへ"
emoji: "⚠️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["git", "エラー", "ざっくり解説"]
published: true
---
## はじめに
`git add`を使っていたら謎の警告が表示される。
```bash
warning: LF will be replaced by CRLF in xxx/xxx.md.
The file will have its original line endings in your working directory
```

VScodeのソース管理からステージングしたら何も表示されない。
何がおかしいのやら？？

## エラーを読んでみる
エラーを見てみるとどうやら以下のようなもの。

Git「このファイルもともと"LF"やないか！！」
Git「しゃーないから勝手に"CRLF"に変えたるわ！」

何してくれてんねん。てかそもそも LF と CRLF ってなんやったっけ？
耳には残ってるねんな。。

## LFとCRLF
ざっくり説明すると
- 2つともOSでの改行や空白文字の表記ルール
  - Linux: LF
  - Windows: CRLF
  - MacOSではCRがある
- VScodeの環境設定で改行文字をCRLFの`\r\n`からLFの`\n`にしている
- → WindowsやからGitに勝手にCRLFに変更させられた

全体を見てみたらOSで表記ルールが違うせいでテキスト表示がバグる可能性がある。
このバグを未然に防ぐためにこんなお節介掛けてくれたんやな。。ありがとう。。

やけど余計なお世話や！！

## 解決法
以下のgitコマンドをちょちょいのちょいよ！
```bash
git config --global core.autocrlf false
```

やっぱconfig系のコマンド使うんやな！
コマンドからも何しているか分かりやすくて助かるわぁ～

Gitの親切にはめちゃおおきにやけど、今回みたいに余計なお世話もあるからびっくりするわね

## 参考
- [Windows git "warning: LF will be replaced by CRLF", is that warning tail backward? - Stack Overflow](https://stackoverflow.com/questions/17628305/windows-git-warning-lf-will-be-replaced-by-crlf-is-that-warning-tail-backwar)
- [【備忘録】改行コード「CR」「LF」「CRLF」の違い #改行コード - Qiita](https://qiita.com/sbeleg_77/items/833de09f7bca24bc8ab8)
