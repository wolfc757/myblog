---
title: "D3.js(V4)を触ってみた(2)"
description: "いろんなグラフを描いてみたかったんや(2回目)"
featured_image: "/images/blog6/circle.png"
date: 2017-11-19T16:26:59+09:00
draft: false
tags: ["d3js","メモ"]
---

D3.jsを触ってみたパート2です！SVGを扱ってブログを書いたりするやつです。　　

<!--more-->

今回のも[ドットインストール](https://dotinstall.com/lessons/basic_d3js)を参考にしながら進めました。  

ちなみに前回基礎的な使い方の部分を[D3.js(V4)を触ってみた(1)](https://blog.wolfc757.net/posts/blog5/)に書いたので全くの初めての方は良ければ参考にしてください。  

## 雛形

今回使う雛形は以下のを使います。  

```
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="utf-8">
    <title>D3jsの練習</title>
</head>
<body>
    <script src="https://d3js.org/d3.v4.min.js"></script>
    <script src="https://d3js.org/d3-selection-multi.v0.4.min.js"></script>
    <script>
        // ここにこねこね書く！
    </script>
</body>
</html>
```

これ以降のコードは `ここにこねこね書く！` と書いてあるところに書いてください。

## データから円を書く  

svgを作ってその中にdatasetが半径になる円を描いています。  

```
// 円の半径
var dataset = [11,25,46,30,33];
// svg領域
var w = 500;
var h = 200;

// svgを追加
var svg = d3.select("body").append("svg")
    .attr("width",w)
    .attr("height",h);

// 円を追加
svg.selectAll("circle")
    .data(dataset)
    .enter()
    .append("circle")
    .attrs({
        cx:function(d,i){return 50+(i*100);},
        cy: h/2,
        r: function(d){return d;},
        fill:"red"
    });
```

こんな感じ
![circle](/images/blog6/circle.png "circle")

## アニメーションをつける

アニメーションは `transition` の後につけていきます。  

`delay` はアニメーションが始まるまでの時間  
`ease` はアニメーションの種類（今回はバウンドするアニメーション）  
`duration` はアニメーションをしている時間  

を示しています。  

```
var dataset = [11,25,46,30,33];
var w = 500;
var h = 200;

var svg = d3.select("body").append("svg")
    .attr("width",w)
    .attr("height",h);

svg.selectAll("circle")
    .data(dataset)
    .enter()
    .append("circle")
    .transition()
    .delay(function(d,i){
        return i * 300;
    })
    .ease(d3.easeBounce)
    .duration(1000)
    .attrs({
        cx:function(d,i){return 50+(i*100);},
        cy: h/2,
        r: function(d){return d;},
        fill:"red"
    });
```

easeについては[ここ](https://bl.ocks.org/d3noob/1ea51d03775b9650e8dfd03474e202fe)で様々なアニメーションのサンプルが見れるのでみて見るといいと思います。  


## 最初と最後の状態の指定

最初と最後の状態を指定するには `on` を使います。  
最初の状態は引数に `start` を
最後の状態は引数に `end` を指定して状態を指定します。  

```
var dataset = [11,25,46,30,33];
var w = 500;
var h = 200;

var svg = d3.select("body").append("svg")
    .attr("width",w)
    .attr("height",h);

svg.selectAll("circle")
    .data(dataset)
    .enter()
    .append("circle")
    .transition()
    .delay(function(d,i){
        return i * 300;
    })
    .duration(1000)
    .on("start",function(){
        d3.select(this).attrs({
            fill:"green",
            r:0,
            cy:h
        });
    })
    .attrs({
        cx:function(d,i){return 50+(i*100);},
        cy: h/2,
        r: function(d){return d;},
        fill:"red"
    })
    .on("end",function(){
        d3.select(this)
            .transition()
            .duration(800)
            .attrs({
                fill:"pink",
                r:0,
                cy:0
            });
    });
```

## イベントを設定

これも先ほどと同じ `on` を使います。  

マウスが乗った時の処理は `mouseover`  
マウスが外れた時の処理は `mouseout`    
クリックした時の処理は `click`  

を引数で渡してあげるとなってくれます！  


```
var dataset = [11,25,46,30,33];
var w = 500;
var h = 200;

var svg = d3.select("body").append("svg")
    .attr("width",w)
    .attr("height",h);

svg.selectAll("circle")
    .data(dataset)
    .enter()
    .append("circle")
    .attrs({
        cx:function(d,i){return 50+(i*100);},
        cy: h/2,
        r: function(d){return d;},
        fill:"red"
    })
    .on("mouseover",function(d){
        d3.select(this).attr("fill","orange")
    })
    .on("mouseout",function(d){
        d3.select(this).attr("fill","red")
    })
    .on("click",function(d){
        var rs = d3.select(this).attr("r");
        alert(rs);
    });
```

## 最後に
今回、2記事でドットインストールで学んだことをメモ書こうと思ったんですがやりたいこととしてはここぐらいまでの内容のメモがあったらいいかなと思って今回のメモはここまでにしておこうと思います。  

すごくざっくりとしたメモなんで時間がある方は[ドットインストール](https://dotinstall.com/lessons/basic_d3js)の方を見るのをオススメします。(棒グラフとか書き方等もありました)  

D3.jsでやりたいことができそうな雰囲気なのでこねこね学んで行こうと思います！  

ではでは！


## 参考
- Data-Driven Documents  
https://d3js.org/
- ドットインストール D3.js入門
https://dotinstall.com/lessons/basic_d3js
- D3.js ドットインストールはV3だけどV4でやってみた
https://qiita.com/chamao/items/1f324e32ccbd547046b1
- Transition Easing Comparison in v4  
https://bl.ocks.org/d3noob/1ea51d03775b9650e8dfd03474e202fe




