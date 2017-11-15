---
title: "公開したサイトをhttps化してみた"
description: "Github Pages + cloudflare + 独自ドメイン"
featured_image: "/images/blog4/cloudflare.png"
date: 2017-11-15T12:25:14+09:00
draft: false
tags: ["HUGO","してみた","メモ","Github Pages","ssl"]
---

HUGOで作成したサイトをGithub Pages + 独自ドメインで公開していたのですがhttps化した時に思っていたよりコケてしまったのでその方法についてメモを書いておきます。

<!--more-->

今回はcloudflareというサービスを利用しました。  
負荷分散等で使われるものみたいですが無料でSSLが使える機能もあったので利用させてもらいました。  

## cloudflareのアカウントを取りドメインを登録

https://www.cloudflare.com/  
アカウントをとって自分の契約した登録したいドメイン名を登録します。  

## DNSの変更
今回自分は、お名前.comで登録を行ったのでお名前.comのDNSからcloudflareのDNSに変更しました。  

cloudflareのDNSのアドレスは `DNS` の `Cloudflare Nameservers` という項目の中にあります。  

## DNSの設定
cloudflareの `DNS` の `DNS Records` という項目から設定します。  
`CNAME`でも`Aレコード`でもどちらでもできるといった記述をみたのですが`CNAME`では上手く行かなかったので`Aレコード`で設定しました。　 

![dns設定](/images/blog4/dns.png "dns")
こんな感じ

## HSTSの設定
cloudflareの `Crypto` の `HTTP Strict Transport Security (HSTS)` の項目を変更します。  
自分は[参考にしたブログ](https://qiita.com/noraworld/items/89dd85a434a7b759e00c)と同じく以下のような設定にしました。　　

![hsts設定](/images/blog4/hsts.png "hsts")
こんな感じ

## HTTPSへのリダイレクト
cloudflareの `Page Rules` からリダイレクトの設定を行います。  

![リダイレクト](/images/blog4/https.png "リダイレクト")
こんな感じ  

ここで設定している `Always Use HTTPS` はDNSがcloudflareのになってないと表示されない場合があるみたいなので表示されなかったらまったり待ちましょう。

一応こんな感じでHTTPS化ができました！  

## 最後に

なかなか最初は表示されたり表示されなかったりと不安でしたが放置してたら動くようになったので気長に待つことも大事なのかなと思いました。  

ではでは

## 参考
- カスタムドメインの GitHub Pages で HTTPS を使う  
https://qiita.com/superbrothers/items/95e5723e9bd320094537
- CloudflareでGitHub PagesをHTTPS化  
https://rcmdnk.com/blog/2017/01/03/blog-github-web/
- Troubleshooting custom domains
https://help.github.com/articles/troubleshooting-custom-domains/

