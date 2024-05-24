---
title: "サイトをPWA対応させる時のチェックリスト"
emoji: "✅"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["PWA", "checklist"]
published: false
---
私が作ったWebアプリのいくつかはPWA対応させている。
そんな時に

そんな時に以下の記事を読んだので、自身のためにも要約したいと思う。
https://web.dev/articles/pwa-checklist?hl=ja#why_2

また、上記記事以外にも有用なものがあったので、それらも一緒にまとめたい。

PWAが分からない人は[プログレッシブ ウェブアプリとは  \|  Articles  \|  web\.dev](https://web.dev/articles/what-are-pwas?hl=ja)を読むと良い。


# PWAアプリのインストールを簡単にする
これがPWA導入にあたって最大の壁だと思っている。

- [PWAインストールの体験を向上させるTips｜りょーた ❖ DESIGN engineer](https://note.com/ryotanny/n/ne47e5618a867)
- [PWA をインストール可能にする - プログレッシブウェブアプリ (PWA) | MDN](https://developer.mozilla.org/ja/docs/Web/Progressive_web_apps/Guides/Making_PWAs_installable#%E3%83%87%E3%82%B9%E3%82%AF%E3%83%88%E3%83%83%E3%83%97%E3%81%A7%E3%81%AE_a2hs)

## PWAアプリをApp Storeに対応させる
PWAアプリをGoogle PlayやApple Storeに出店する事も可能だ。
https://web.dev/articles/pwas-in-app-stores?hl=ja

しかし少しの手間がかかる。以下のPWABuilderを使えばよい。
https://www.pwabuilder.com/
