---
title: "HUGOで作成したサイトをGithub Pages + 独自ドメインで公開してみた"
description: ""
featured_image: "/images/blog3/githubpage.png"
date: 2017-11-10T15:37:05+09:00
draft: false
tags: ["HUGO","してみた","メモ","Github Pages"]
---

HUGOで作成したサイトをGithub Pages + 独自ドメインで公開した方法についてメモを書いておきます。

<!--more-->

ここではHUGOのサイトを作った前提で進めていきます。
HUGOでのサイトの作り方等は[こちら](http://blog.wolfc757.net/posts/blog2/)にメモを書いています。  

今回の内容はHUGOのサイトの[ここ](https://gohugo.io/hosting-and-deployment/hosting-on-github/)を参考にしています。  

## HUGOでの設定

`docs` のフォルダを公開するのでソースを `docs` に出すように
設定ファイルの `config.toml` に以下を追加。  
それとbaseURLをGithubのURLに変更します。  
```
publishDir = "docs"
```

その後ビルド
```
$ hugo
```

あとはgithubのリポジトリを作りそこにpushする。  
```
$ git add .
$ git commit -"好きなコメント”
$ git remote add origin [自分のリポジトリurl]
$ git push -u origin master
```

## Githubの方での設定

Githubの先ほどpushしたリポジトリの `setting` の `Github Pages` の項目を  
`master branch /docs folder` に変更する。  

![setting](/images/blog3/setting.png "setting")

するとGithub Pagesで公開できます！  

## 独自ドメインの設定
ここではお名前.comで、すでにドメインを取っている程で進めます。 ここは[このページ](https://gyoza.beer/post/2017-05-14-custom_domain/)を参考にさせてもらいました。  

先ほど設定した `setting` の Github Pages の中にある  
`Custom domain` に設定したいURLをセットします。   
自分は今回 `blog.wolfc757.net` というURLを利用しました。　 

![setting2](/images/blog3/setting2.png "setting2")  
するとCNAMEファイルがコミットされるようです。  

その後、お名前.comのDNSレコード設定より以下のような設定を行えば独自ドメインで見ることができます！  

![setting3](/images/blog3/setting3.png "setting3")  

## 最後に

思っていたよりもサックっとできました。  
あとは、ブログをこねこね書いていくことと  
https化したいなと思います！  

ではでは

## 参考

- Host on GitHub  
https://gohugo.io/hosting-and-deployment/hosting-on-github/
- Github Pagesを独自ドメインで公開する  
https://gyoza.beer/post/2017-05-14-custom_domain/