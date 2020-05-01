---
layout: post
title: "Octopressで表を挿入する"
date: 2016-06-16 10:52:50 +0900
author: Masato Nike
comments: true
tags: ['Octopress', 'Markdown']
---
昨日の投稿で表を入れようとして、少しはまったので、メモ代わりに書いておきます。  
  
## 1. 表の作り方
  
Markdownでの表の作り方は簡単で、以下のようにすれば、それぞれ左寄せ、中央寄せ、右寄せになります。  
  
<pre class="brush: xhtml;">
|分類|項目|価格|
|:--|:--:|--:|
|果物|りんご|100|
|果物|バナナ×10|1000|
|野菜|セロリ|88|
|飲み物|牛乳|200|
</pre>
  
<!--more-->
以下が実際に作成される表です（カスタマイズ済みです）。  
  
|分類|項目|価格|
|:--|:--:|--:|
|果物|りんご|100|
|果物|バナナ×10|1000|
|野菜|セロリ|88|
|飲み物|牛乳|200|
  
## 2. 表のカスタマイズ
デフォルトの表では以下のように表示されます。  
  
![Octopressでの表](/images/blog/2016/06/16/octopress_table.jpg)

これでは罫線も背景色も何もなく味気ないので、"/stylesheets/table.css"というファイルを用意し、以下のようにします。

``` css
* + table {
    border-style:solid;
    border-width:1px;
    border-color:#e7e3e7;
    margin: 10px 0 30px 0;

* + table th, * + table td {
    border-style:dashed;
    border-width:1px;
    border-color:#8888AA;
}

* + table th {
    border-top:    1px #666688 solid;
    border-bottom: 2px #666688 solid;
    font-weight:bold;
    background-color: #C0C0C0;
    padding: 2px 9px;
}

* + table td {
    border-bottom: 1px #666688 solid;
    background-color: #F0F0F0;
    padding: 0 10px;
}

* + table th[align="left"], * + table td[align="left"] {
    text-align:left;
}

* + table th[align="right"], * + table td[align="right"] {
    text-align:right;
}

* + table th[align="center"], * + table td[align="center"] {
    text-align:center;
}
```

そして、"source/_includes/head.html"に以下の一行を加えます。  

<pre class="brush: xhtml;">
<link href="{{ root_url }}/stylesheets/table.css" rel="stylesheet" type="text/css">
</pre>

以上で、罫線や背景のある表が作成できるようになります。
