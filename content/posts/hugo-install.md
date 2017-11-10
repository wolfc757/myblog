---
title: "HUGOでブログを作成してみた"
description: ""
featured_image: "/images/blog2/hugo1.png"
date: 2017-11-10T05:18:11+09:00
draft: false
tags: ["HUGO","してみた","メモ"]
---

このブログをHUGOで作成してみたのでそのメモを書いておきます。  

<!--more-->

# HUGOとは？

![HUGOサイト](/images/blog2/hugo.png "HUGOサイト")

[HUGOサイト](https://gohugo.io/)

HUGOとはGo言語で作られた静的サイトジェネレータです。  
早いのが特徴のようです。


今回はこの中の[クイックスタートのページ](https://gohugo.io/getting-started/quick-start/)を参考にしながらブログを作成してみました。



# HUGOのインストール

macの方で[Homebrew](https://brew.sh/)を使っている方は以下の一行でインストールが可能です。

```
$ brew install hugo
```

Windowsの方は[Chocolatey](https://chocolatey.org/)というのでインストールできるようです。

インストールの確認は以下のコマンドで行います。
```
$ hugo version
```



# 新しいサイトを作成

```
$ hugo new site [好きなディレクトリ名]
```
上記の手順で作成できます。  
私は以下のように作成しました。

```
$ hugo new site myblog
```



# テーマを追加

好きなテーマを追加します。  
テーマは[こちら](https://themes.gohugo.io/)に一覧があります。  
今回はサイトに書いてある[Anankeテーマ](https://themes.gohugo.io/gohugo-theme-ananke/)を使用しました。  

```
$ cd myblog
$ git init
$ git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
```

その後設定ファイルに何のテーマを使ったかを記述します。  
```
$ echo 'theme = "ananke"' >> config.toml
```



# コンテンツを追加

```
$ hugo new posts/hello-world.md
```
これでファイルを追加できます。  

Hugoサーバを起動してみます。　　
```
$ hugo server -D
```
すると[http://localhost:1313/](http://localhost:1313/)ここでそのサイトを見ることができます。


![こんな感じ](/images/blog2/hugo-try1.png "こんな感じ")
こんな感じになりました。



# テーマをカスタマイズ
タイトルなど変更するために`config.toml`を変更します。  
好きなエディタ等で開くと以下のようになっているかと思います。
```
baseURL = "https://example.org/"
languageCode = "en-us"
title = "My New Hugo Site"
theme = "ananke"
```

ここの`title`を変更すると以下のようになりました。　　
![こんな感じ](/images/blog2/hugo-try2.png "こんな感じ")  

画像等の変更は`static/images`の中に変えたい画像を入れ、`config.toml`の下に
```
[params]
    featured_image = "/images/pc.jpg"
```
のような記述をしてあげると変更できました。

その他のカスタマイズは[テーマ](https://themes.gohugo.io/gohugo-theme-ananke/)の説明に載っています。　　

# 最後に

ここまでで何となくブログの作成ができました。  
すごく簡単にできて驚きです。
ただ、まだローカルでしか動かしていないので実際に外から見ることはできません。  
次回の記事で公開する方法などを書こうと思います。  

ではでは