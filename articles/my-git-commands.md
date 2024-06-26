---
title: "【不定期更新】Gitコマンドの細道"
emoji: "🪄"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Git", "コマンド集", "チートシート"]
published: true
---
## まえがき
普段はVScodeのソース管理でGitを使っているTim daikです。
以前はVScodeを使ってMarkdownを書いていたのですが、少し前にObsidianにハマってからMarkdownを書くときはマークダウンエディタを使用しています。

VScodeから浮気して出てきた課題が「Git操作がやりにくいことこの上ない！！」です。
前述のとおりVScodeには左側のサイドバーにあるソース管理からGit操作を行えます。
浮気先のObsidianにはもともとGit操作用の機能が無いものの、プラグインが豊富にあるため、Gitの拡張機能を使用することで解決できます。
しかし、コミットやプッシュなどの操作をGitを使用せずにプラグイン用のJavaScriptで実行しているため、操作が重いなどUIが気に喰わないなど使いずらいです。

そこでこれも機会だな、と思い、Git操作をCUI上で完結できるようになろう！と考えました。
他の理由として、
- Gitについての理解を深められる
- Gitの機能を最大限に活用できる
- なんやかんやCUI上での操作のほうが早いだろう

などがあります。
結果的には操作速度が向上しましたし、Gitへの理解もちょっとずつ深められています。
しかし、コマンドの種類がなんせ多いので、忘れてしまいます★
そこでこの記事では筆者である私が よく使う・たまに使う・あまり使わないけど必要 の3つに分類したGitコマンドたちを紹介しています。

この記事を
- GitをCUI上で操作したい人々
- Gitのさまざまな機能を使いこなしたい欲のある人々
- Gitのコマンド覚えられねえよ。。な人々
- 上記3つが当てはまる筆者

に捧げます。

> 普通に最初はVScode上などGUIのほうが操作しやすいので、コマンド操作を楽しむ感覚で取り組むと良いと思います。
> VScodeのほうが楽な場合が多いので、ムリにコマンドラインで操作しなくても大丈夫です。
> しかし、ところどころコマンド操作は必要なのでチートシートみたいにご利用ください。

## よく使う
自分がよく使うコマンド集です。
他の皆さんも使いがちなラインナップとなっているはずなので、特にオプションをご参考下さいませ。

### `git commit`
いわずもがなコミットをするためのコマンドです。
通常はコミットメッセージをつけたりとオプションを使うので、使いがちなオプションまとめます。

<!-- TODO -->
🚧コマンドオプションを追加する

### `git status`: 各ファイルの変更状況を把握する
各ファイルが
- 新規ファイルなのか削除ファイルなのか
- 名前を変更しただけなのか
- ステージングされているのか否か

など、変更状況は必須レベルに確認したいですね。
そんな時は`git status`が使えます。
```bash
git status
```

いつもVScodeの「Git History」という神拡張機能に頼っているため、ぶっちゃけ`git status`の凄みが感じられにくい今日この頃です。
ただし地味に使うので感謝は忘れません。

### `git diff`: ファイルの変更点を確認する
ファイルを編集したは良いが、どこをいじったのかが分からなくなることが多い。
そこでファイルの変更点、差分を表示してくれるのが`git diff`コマンドです。

#### :construction: コマンドオプション...
aaaa...

### `git reset`: コミット履歴に対して取り消しを行う
主にステージングの取り消しや、過去のコミット時点に復帰する場合はこのコマンドを使用すると良いです。
過去コミットに復帰する際は`git log`でその時点で表示されるハッシュ値`commit-hash-val`を確認し、以下のコマンドに代入します。
```bash
git reset --hard <commit-hash-val>
```

似たようなコマンドに`git restore`があります。
ステージングの取り消しはこのコマンドでも可能ですが、このコマンドはファイルの具体的な変更に対しての操作に向いています。
例えば、ステージングエリアで特定のファイルのみ変更を取り消すなどです。

### `git restore`: ステージングの取り消しを行う
先ほど紹介したばかりですが、このコマンドを使用することで、うっかりステージングしてしまったファイルのステージングを取り消しできます。

### `git log`
リポジトリに記録しているコミット履歴を見ることが出来るコマンドです。
VScodeでは拡張機能のGit Historyが非常に見やすくて、よく使うのですが、VScode以外の例えばObsidianなどのMarkdownエディタを使う時にコマンドを使いたい時が多いです。
また、コマンドオプションを使うことでかなりログをカスタム表示できるので、これらをまとめておきます。

#### `q`: 終了するとき
まず`git log`を使用するにあたって、表示の終了方法を知っておいたほうが良いです。
どういうことかと言うと、`git log`の出力を見て頂ければいいと思います。

![](/images/my-git-commands/my-git-commands-1.gif)

そう、終了コマンドが分からなくて**永遠にログを見させられます。**
ということで終了コマンドをまず覚えましょう。

```bash
q
```

半角`q`を入力するだけ。ホンマにこれだけ。。

#### `-n`: 表示コミット数の制限
通常`git log`コマンドを使用すると、全てのログが表示されるまでスクロールしていく必要があります。
全ログが不要で、直近のコミットだけを確認したいときは以下のようにします。

```bash
git log -n 5
```

今回は最新5つのコミットが表示されます。
`-n`オプションの後に任意の数字を入力すると、その数字分だけのコミットが表示されます。

<!-- TODO -->
🚧上に他のよく使うコマンドも随時追加

## たまに使う
頻繁には使いませんが、かなり使うので覚えておきたいコマンド集です。

<!-- TODO -->
🚧上にコマンドを随時追加

## あまり使わないけど必要
ホンマに使わないですが、いざという時に覚えておくと便利、否、覚えておかないといけないコマンド集です。

### `git rm -r --cached`: コミット済みのファイルを`.gitignore`に追加したい時
`.gitignore`にファイルを追加しても、追跡対象になっていた時がたまにあります。
このままでは`.gitignore`にファイル・フォルダ名を書いたところで、全然Gitコミットとして記録されていくので、追跡対象外にしてやる必要があります。

```bash
git rm -r --cached <file-or-folder-name>
git rm -r --cached ./README.md # 例: README.mdを追跡対象外に加えるとき
```

これでGitのコミット記録から外されますが以前のコミット履歴は残ってしまうので、コミット履歴を削除したい場合は、後述する[コミット履歴を削除したい時](#コミット履歴を削除したい時)を参考にしてください。

### コミット履歴を削除したい時
🚧力尽きたので随時追加

### `git config core.quotepath false`: `git status`での日本語ファイル名の文字化けを直したい時
`git status`コマンドを使ってファイルを表示する際に、ファイル名が日本語のものが含まれていると文字化けすることがあります。
なんとなくですが以下のようにファイル名が表示されます。
```bash
"\287\341\202\109\280\377\295.pdf"
```

この文字化けを解消するには以下のコマンドで設定を変更してやる必要があります。

```bash
git config --global core.quotepath false
```

`--global`オプションで現在のリポジトリだけでなく、全体の設定として扱えます。
基本的にはグローバルで問題ないでしょう。

### `git diff`でも文字化けするのを直したい

<!-- TODO -->
🚧上にコマンドを随時追加

## 参考
- [【Git入門】git log の使い方とオプション一覧（コミット履歴を確認する） | 初心者向け完全無料プログラミング入門](https://26gram.com/git-log)
- [git logコマンドを終了する方法 #初心者 - Qiita](https://qiita.com/EasyCoder/items/7a0fc2146a9b07929b67)
- [.gitignoreに記載したのに反映されない件 #Git - Qiita](https://qiita.com/fuwamaki/items/3ed021163e50beab7154)
- [【Git】やっちまったコミットを戻したい時のTips](https://zenn.dev/nekoniki/articles/f238efa56eb869#revert%E3%82%92%E4%BD%BF%E3%81%86%E5%A0%B4%E5%90%88)
- [【Git】git status で変更状況を確認する方法 #Git - Qiita](https://qiita.com/sun_tomo/items/2aa7c4b2f6534fc0f0b3)
- [[git]git statusコマンドで日本語の文字化けを解消する | akamist blog](https://akamist.com/blog/archives/1160)
- [git diff や git status での日本語の文字化けを防ぐ (core.page, core.quotepath) - まくまく Git ノート](https://maku77.github.io/p/cj2uie9/)
- [git reset と git restore の違いを理解しよう #Git - Qiita](https://qiita.com/yamazaki_25/items/eace7d15ec16d4c6d822)
- [忘れやすい人のための git diff チートシート #Git - Qiita](https://qiita.com/shibukk/items/8c9362a5bd399b9c56be)
