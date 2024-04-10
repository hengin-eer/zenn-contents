---
title: "Astroで構築した静的サイトを独自ドメインでデプロイしようとしたら思いのほか苦労した話"
emoji: "🥵"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Astro", "Netlify", "GitHubActions", "独自ドメイン"]
published: false
---
# 独自ドメインを初めて取得！！
【実績解除】独自ドメインを取得した話 みたいな記事を別で書く。
これのリンクを貼って、補足する程度。

**Xserver Domainで取得した旨のみ強調する。**

# 連携が楽ちんなNetlifyを試すが..
Astroのデプロイでよく使っているNetlifyを選んだ。
デプロイも簡単だし、mainブランチへPushするだけで更新してくれるのは神！！
環境変数の設定も楽々！

## 沼ったポイント
- 独自ドメインの設定が面倒くさい
  - 設定自体は超簡単！（ドメイン入力したら出てくるネームサーバーをXserver Domain側で設定するだけ）
  - 独自ドメインを使うにはネームサーバーをNetlifyにする必要
  - → Netlifyのドメイン管理システムを使うには課金必須
    - 課金無しにサブドメインの発行ができない！！

（個人開発者にとってサブドメインは神だと語る）

ざっくりまとめると、サブドメインが使えなくなるためNetlifyから離れることに。。

# GitHub Actionsを使うことに
となれば、どうせGitHubにコード置いているわけだし、GitHub Pagesを使ってしまえ！
workflowも少し分かる & Astro公式が見本出しているので楽勝だなあ～😆
https://docs.astro.build/ja/guides/deploy/github/

しかし、、

## 沼ったポイント
- 環境変数の設定
  - GitHub Actionsでエラーを吐きまくり
  - JAMstack時の環境変数の設定方法が分からなかった
  - そもそも""で括ってしまったらアカンかったことに気づかなかった
- 独自ドメイン
  - 記事が無く、ドキュメントを見ないといけなかった（要精進）

### 環境変数の設定に苦しむ
「環境変数なんてリポジトリのシークレットに設定すれば良いんでしょ？？ はよデプロイ終わらんかな」
なんて軽い気持ちでデプロイを眺めていたら、期待通りデプロイ処理が爆速で終わりました。いや、止まりました🛑

内心「？？？」と唖然ながらもログを確認してみます。
どうやらContentfulからデータを取得できていないようです。

「これは環境変数のせいやな」と直ぐに分かったのは良かったのですが、これに2日苦しみました。
プログラマの皆さんならデプロイの時ほどプレッシャーから解放されるというか、報われるというか、ワクワクすると思います。
しかしこんだけデプロイが失敗でもすれば流石にストレスが溜まってきますね😠

最終的には、以下の記事がこの苦しみから救ってくれました。。ホンマに感謝です🙏
https://qiita.com/sho_fcafe/items/6ef087cb3b1586464175

何が悪かったって、どうやらworkflowのYAMLファイル内に環境変数に関する記述を追加する必要があるそうです。
以下のようにしてGitHub上で設定したシークレットを環境変数として認識させられます！

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout your repository using git
        uses: actions/checkout@v4
      - name: Install, build, and upload your site
        uses: withastro/action@v1
        with:
          path: .
          node-version: 20
          package-manager: npm@latest
        env: # GitHub上のシークレットを環境変数として認識させる
          CONTENTFUL_SPACE_ID: ${{ secrets.CONTENTFUL_SPACE_ID }}
          CONTENTFUL_DELIVERY_TOKEN: ${{ secrets.CONTENTFUL_DELIVERY_TOKEN }}
```



## 参考
- [全くの初心者がnetlifyとX Domain(X Server)でサーバーを独自ドメイン化した話 · Daizyu.com](https://daizyu.com/posts/2020-05-07-001/)
- [DNSとは？DNSの仕組み | Cloudflare](https://www.cloudflare.com/ja-jp/learning/dns/what-is-dns/)
- [AstroサイトをGitHub Pagesにデプロイする | Docs](https://docs.astro.build/ja/guides/deploy/github/)
- [カスタムドメインとGitHub Pagesについて - GitHub Docs](https://docs.github.com/ja/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages)
- [GitHub Pages サイトのカスタムドメインを管理する - GitHub Docs](https://docs.github.com/ja/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-a-subdomain)
- [GitHub Actionsで静的ジェネレートした時に環境変数を使う #Nuxt - Qiita](https://qiita.com/sho_fcafe/items/6ef087cb3b1586464175)
