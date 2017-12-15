---
title: "D3.js(V4)を使ってドラッグした時の動きを実装する"
description: "色々動かせたらなんかテンション上がらん？笑"
featured_image: "/images/blog7/base.png"
date: 2017-12-15T18:22:00+09:00
draft: false
tags: ["d3js","メモ"]
---

SVGの要素をドラッグしてみた内容です。

<!--more-->

今回はSVGの要素をドラッグして動かせたらなって感じで作りました。

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
        // windowのサイズ
        window_x = window.innerWidth;
        window_y = window.innerHeight;

        // 円の半径
        r = 30;

        // svgの作成
        var svg = d3.select("body").append("svg").attrs({
            width:window_x,
            height:window_y
        });

        // 円の作成
        var circle = svg.append("circle")
                .attrs({
                    r: r,
                    fill: "lightgreen",
                    transform: "translate(" + window_x/2 + "," + window_y/2 + ")"
                });
        // ここにこねこね書く！
    </script>
</body>
</html>
```

簡単に説明しておくと画面の中央に緑の円ができている状態です。  
これ以降のコードは `ここにこねこね書く！` と書いてあるところに書いてください。


こんな感じ
![base](/images/blog7/base.png "base")

# リスナーの追加
```
// イベントをセット
circle.call(d3.drag()
    .on("start",dragstarted)
    .on("drag", dragged)
    .on("end",dragended)
);
```
このようにセットします。  
`on` の第一引数は`タイプ`,第二引数は`リスナー`です。  
イベントリスナーが同じタイプと名前で登録されている場合は新しいリスナーが追加される前に既存のリスナーが削除されます。  

タイプについては以下の三つがあるようです。  

- `start` ・・・ 新しいポインタがアクティブになった後
- `drag` ・・・ アクティブなポインタが移動した後
- `end` ・・・　アクティブなポインタが非アクティブになった後

# リスナーの作成

```
// 新しいポインタがアクティブになった後に呼ばれる関数
function dragstarted(d){
    console.log("dragstarted");
}
// アクティブなポインタが移動した後に呼ばれる関数
function dragged(d) {
    console.log("dragged");
    d3.select(this).attr("transform", "translate(" + d3.event.x + "," + d3.event.y + ")");
}
// アクティブなポインタが非アクティブになった後に呼ばれる関数
function dragended(d){
    console.log("dragended");
}
```
このように作成しました。  

実行結果は以下のようになっています。　　

<p data-height="265" data-theme-id="0" data-slug-hash="wpaOma" data-default-tab="js,result" data-user="wolfc757" data-embed-version="2" data-pen-title="D3.js drag sample" class="codepen">See the Pen <a href="https://codepen.io/wolfc757/pen/wpaOma/">D3.js drag sample</a> by yuu (<a href="https://codepen.io/wolfc757">@wolfc757</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

# 最後に
今回試したもののソースコードは[ここ](https://gist.github.com/wolfc757/3b954563e82790d77d088fc21c820e40)に置いておきます。サンプルコードをみてるとCanvasで行ってたりする例もあったのでいろいろと使えそうですね！  
では！  

# 参考
- D3.jsドキュメント(d3-drag)  
https://github.com/d3/d3-drag/blob/master/README.md
- Circle Dragging IV  
https://bl.ocks.org/mbostock/ec10387f24c1fad2acac3bc11eb218a5
- Circle Dragging II  
https://bl.ocks.org/mbostock/c206c20294258c18832ff80d8fd395c3
- d3.js入門　ドラッグイベント  
http://jsdo.it/_shimizu/hszt
