---
title: "Googleの旧Nearby ShareをダウンロードしようとしたらEdgeとChromeで対応が違くて泣いた"
emoji: "🥲"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["News", "NearbyShare"]
published: true
---
:::message
後で個人ブログに移動するかもです。
:::

GoogleのNearby ShareがQuick Shareに変わったらしいので、Windows版をダウンロードしようとしたら、Microsoft Edgeへの露骨な対応が見られたので愚痴ります。
ただこれだけです。

https://twitter.com/tim_daik/status/1779142565377544665

## Quick Shareという名前に変わったらしい
どうやら4/9をもって、Nearby ShareからQuick Shareへと新しくなったらしいです。

https://www.android.com/better-together/quick-share-app/

ぶっちゃけ変更点は分かりませんが、おおよそ「Material Design 3 に対応してきた」みたいです。
接続時に表示される円状プログレスバーのアニメーションについての変更が取り上げられていました。
詳しくは以下の記事を見ると良いです。

https://9to5google.com/2024/04/09/quick-share-file-transfer-progress-animation/

以前のWindows版Nearby Shareはプレビュー版であり、これが突然使えなくなったことでアップデートに気づきました。

## Edgeでアクセスするとダウンロードできない😢

https://www.android.com/better-together/quick-share-app/

ここからWindows版がダウンロードできます。
「さてさて、ようやくWindows版も正式対応かあ～」と喜んでいたのもつかの間、なんかダウンロードできないんですけど。。

![](/images/news_cannot-access-quickshare-in-edge/news_cannot-access-quickshare-in-edge-1.png)

Email me a link の下に書いてある注意書きを見てみると、以下のように書かれていました。

> It seems your device is not compatible with Quick Share for Windows.
> For Windows computers running a 64-bit version of Windows 10 and up. ARM devices not supported.

> お使いのデバイスはQuick Share for Windowsに対応していないようです。
> 64ビット版のWindows 10以上を実行しているWindowsコンピュータが対象です。ARMデバイスには対応していません。

「なんやと!? プレビュー版では使えていたのに、いざリリース版では使えないってどういうこと？？」
自分の機種は対象であるのに使えないと言われてしまい、さすがに参ってしまいました。
英語でのヘルプ記事も取り敢えず探してみました。
非常に面倒くさいですが、Googleに問い合わせてみようか、とも思いました。

しかしなんとなく勘づきました。

## Chromeで開いてみる
もしかしたら、、と思いChromeでページを開いてみました。
すると、

![](/images/news_cannot-access-quickshare-in-edge/news_cannot-access-quickshare-in-edge-2.png)

🤔「???」
案の定、こちらではダウンロードボタンが表示されていますね!?

どうやらブラウザがEdgeだと意地でもダウンロードさせてくれないようです。
実際、Chromeからダウンロードしたので思惑通りとなっているわけではありますが。。

## 結論
ユーザが不利益を得るような争いはやめてください。
