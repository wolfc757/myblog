---
title: "D3.js(V4)を触ってみた(1)"
description: "いろんなグラフを描いてみたかったんや"
featured_image: "/images/blog5/d3js.png"
date: 2017-11-18T02:57:28+09:00
draft: false
tags: ["d3js","メモ"]
---

D3.jsというデータに基づいてドキュメントを操作するためのJavaScriptライブラリを触ってみたのでメモを残しておきます。

<!--more-->

今回は初めてだったので[ドットインストール](https://dotinstall.com/lessons/basic_d3js)を参考にしながら進めました。


## D3.jsとは
データに基づいてドキュメントを操作するためのJavaScriptライブラリでこのD3はData-Driven Documentsの略みたいです。  

どんなことができるかは[Gallery](https://github.com/d3/d3/wiki/Gallery)等をみてみるとわかりやすいのではないでしょうか？  

## 雛形

今回使う雛形
```
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="utf-8">
    <title>D3jsの練習</title>
</head>
<body>
    <p>hello1</p>
    <p>hello2</p>
    <p>hello3</p>
    <script src="https://d3js.org/d3.v4.min.js"></script>
    <script src="https://d3js.org/d3-selection-multi.v0.4.min.js"></script>
    <script>
        // ここにこねこね書く！
    </script>
</body>
</html>

```
こんな感じの雛形を使って行きます。  
これ以降のコードは `ここにこねこね書く！` と書いてあるところに書いてください。

## 要素を選択

要素を選択するには `select` と `selectAll` を使って行きます。

この雛形の場合bodyタグの中のpタグを全て選択しようとすると以下のようになります。  

```
d3.select("body").selectAll("p");
```

## テキストを変更する

要素のテキストを変えたい時は `text` を使います。  

```
d3.select("body").selectAll("p").text("hello form d3!");
```

変数として分けることもできます。  
```
var p = d3.select("body").selectAll("p");
p.text("hello form d3!");
```

こんな感じ
![text](/images/blog5/text.png "text")

## スタイルを変更する

要素のスタイルを変えたい時は `style` タグを使います。  

```
var p = d3.select("body").selectAll("p");
p.text("hello form d3!");
p.style("font-size","28px");
```

メソッドチェーンでつなげたり複数のスタイルを指定することもできます。
```
var p = d3.select("body").selectAll("p");
p.text("hello form d3!")
    .style("font-size","28px")
    .style("color","red");
```

スタイルを一度に指定することもできます。
```
var p = d3.select("body").selectAll("p");
        p.text("hello form d3!")
            .styles({
                "font-size": "28px",
                "color": "red"
            });
```

こんな感じ
![style](/images/blog5/style.png "style")

## 要素を加える

要素を加える時は `append` を使います。　　

```
d3.select("body").append("p").text("hello4");
```

こんな感じ
![append](/images/blog5/append.png "append")

## 要素を削除

要素を加える時は `remove` を使います。　　

```
d3.select("body").append("p").text("hello4").remove();
```

こんな感じ
![remove](/images/blog5/remove.png "remove")

## データを紐付ける

要素を加える時は `data` を使います。　　

```
var dataset = ["data1","data2","data3"];
var p = d3.select("body").selectAll("p");
p.data(dataset).text(function(d){
    return d;
});

```

こんな感じ
![data1](/images/blog5/data1.png "data1")  

第二引数は要素数らしいのでこんな書き方もできます。　　

```
var dataset = ["data1","data2","data3"];
var p = d3.select("body").selectAll("p");
p.data(dataset).text(function(d,i){
    return i + "つ目のデータ : " + d;
});
```

こんな感じ
![data2](/images/blog5/data2.png "data2")  


## データを紐付ける時に要素数が足りない場合

データを紐付ける時に要素数が足りない場合は `enter` を使います。
足りない分は `append` で加えます。

```
var dataset = ["data1","data2","data3","data4"];
var p = d3.select("body").selectAll("p");
var update = p.data(dataset);
var enter = update.enter();
update.text(function(d){
    return "update : " + d;
});
enter.append("p").text(function(d){
    return "enter : " + d ;
});
```

こんな感じ
![enter](/images/blog5/enter.png "enter")  

## データを紐付ける時に要素数が余る場合

データを紐付ける時に要素数が余る場合は `exit` を使います。  
いらない分は `remove` で消します。　　

```
var dataset = ["data1","data2"];
var p = d3.select("body").selectAll("p");
var update = p.data(dataset);
var exit = update.exit();
update.text(function(d){
    return "update : " + d;
});
exit.remove();
```

こんな感じ
![exit](/images/blog5/exit.png "exit")  

## 最後に
jsを普段全く触らないのですが思っていたよりもサクサク書けてたので楽しかったです。
今回後半部分までは書けなかったので次回後部分（svg部分）を書こうと思います。　　

ではでは！


## 参考

- Data-Driven Documents  
https://d3js.org/
- ドットインストール D3.js入門
https://dotinstall.com/lessons/basic_d3js
- D3.js ドットインストールはV3だけどV4でやってみた
https://qiita.com/chamao/items/1f324e32ccbd547046b1