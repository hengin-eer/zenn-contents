---
title: "useStateのバケツリレーに疲れたからRecoilに入門した。感動した"
emoji: "🪣"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Recoil", "状態管理"]
published: true
date: "2023/9/21"
---
:::message
この記事は2023/9/21に https://hengineer-blog.netlify.app/post/introduction-to-recoil/ で公開された記事をZennにアップロードしたものになるため、情報が古い場合があります。
ご注意下さい。
:::

## まとめ
- ステートのバケツリレーに疲れたらRecoilを使おう
- 導入は__超かんたん__だった
- 思ったより`useState`に近くて驚いた
- 全てのプロジェクトではいらなさそう
- とりあえずやってみる精神は大切

## バケツリレーの限界
Reactを使ってアプリ開発するとき、必須のフックといっても過言じゃない`useState`。
私は今まで`useState`を使ってステート管理してきました。
グローバルステートを使っていなかったのでステート管理を複数のコンポーネントでしたいときは、一番上の親コンポーネントでステートを定義して子コンポーネントに`props`として受け渡していました。
私は今までコンポーネントのネストが多くても3つまでだったため、これでも平気でした。

しかし、ユーザー管理をするアプリケーションを作成したときにバケツリレーがしんど過ぎて困ってしまいました。
ここで初めて`useContext`を知り、しばらくはこれを使っていました。しかし`useContext`を使うと`context`が変更されるたびに親コンポーネントも再レンダリングされることを知りました。また`context`の数だけ`_app.jsx`をプロバイダーで囲うのが嫌になりしました。

なので私はもっと楽にグローバルステートを管理したいと思うようになりました。
そこで前々から聞いていた、Recoilに入門することにしました。
正直Reduxを学ぼうか迷ったのですが、Reduxでは`Store`ですべてのステートを管理することのリスクや、トレンドなどからRecoilが選ばれました。

## いざ入門
さっそくグローバルなステートを管理してやろう、と思い導入しました。
私は`Next.js`に導入したので`Next.js`ベースで説明していきます。基本的にどのReactプロジェクトでも行けると思います。

```bash
npm i recoil
```

インストールしたら以下の作業を行います。
1. `_app.jsx`でコンポーネントを`RecoilRoot`で囲む
2. `src`ディレクトリの下に`States`ディレクトリを作成します（好みによる）
3. ファイルを作成し`Atom`でステートを定義する
4. 任意の場所で呼び出す

軽く説明。

まず`_app.jsx`で`RecoilRoot`を以下のように呼び出します。

```javascript
import '@/styles/globals.css';
import { RecoilRoot } from 'recoil';

export default function App({ Component, pageProps }) {
  return (
    <RecoilRoot>
      <Component {...pageProps} />
    </RecoilRoot>
  )
};
```

次に`/src/States`ディレクトリを作成します。
作成出来たらステートを定義するファイルを作成します。
`userSessionState`を定義したければ`userSessionState.js`という名前が良いでしょう。
実際にやってみましょう！

```javascript
import { atom } from "recoil";

export const userSessionState = atom({
    key: "userSessionState",
    default: false,
});
```

`default`で初期値を設定できます。

それではグローバルステートを使ってみましょう。
ほとんど`useState`と同じように使うことが出来ます。
ただし`useState`とは違い、ステートだけ・ステートを更新する関数だけをそれぞれ呼び出すことが可能です。

```javascript
const [userSession, setUserSession] =  useRecoilState(userSessionState);
const userSession = useRecoilValue(userSessionState); // ステートの取得のみ可能
const setUserSession = useSetRecoilState(userSessionState); // ステートの更新のみ可能
```

`useState`でいう以下のような感じですね。
__ステート定義だけしちゃって、hooksに"Recoil"って付いただけじゃん！！__
思ったよりも簡単でした。

```javascript
const [userSession, setUserSession] = useState(false);
```

Recoilで呼び出しているhooksの引数に、定義してあげたグローバルステートをぶち込むことで使えるようになります。
ありがたいですね。

## プロジェクトに最初から組み込むべき？
ご覧の通り、めちゃくちゃ楽ちんに導入できたRecoil。
グローバルステート管理がこんなに簡単にできるなら、最初からプロジェクトに組み込んでもよさそうです。

見出しの問いに対する私の答えはNoです。
何故か？

- 簡単に導入できるなら後から必要になってからでも良い
- なるべくグローバルステートを使わないようにする
- ボイラーテンプレートとなるから使わなくて済むなら使わない

こんな感じの理由です。

よく「変数のスコープが狭ければ狭いほど良い」と言う言葉を聞きますが、ステートも基本的には一緒だと思います。

あとファイルサイズが肥大化しちゃうので、使わなくて済むなら使わないようにするべきでょう。
ぶっちゃけパーフォンマンスのことを考えないといけないので面倒くさいですが、面倒くさくても改善できるならやらないといけないです。
また、パフォーマンスのことを考えないといけないおかげで、頭を使ってプログラミングできるので楽しいですね。

今回Recoilを触る前は「触ってみたいけど難しそうだしな～時間採らないといけないしな～」と腰が引けてました。
しかし使うキッカケが出来て、実際使ってみたらとても便利や、と気づけました。
なので今回は「とりあえずやってみよう」の大事さを確認できたのも収穫です。
なので新しい技術を取り組むときは思い切って触ってしまったほうが良いと思います！

（ご利用は計画的に）をちょっと頭に入れておけば大丈夫だと思います。

最後は自分の感想になりましたが、以上Recoilに入門してみた記事でした！！
バイバイ👋
