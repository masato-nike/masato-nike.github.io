---
layout: post
title: "さくらインターネットでサーバ構築②"
date: 2016-06-21 05:38:10 +0900
comments: true
tags: ['Build Server', 'CentOS']
---
今回はDNSサーバの構築について書こうと思いますが、
タイトルには『さくらインターネット』と書いていますが、
今回、さくらインターネットでドメインを取得しなかったため、
さくらインターネットはあまり関係ないです。  
<!--more-->
## 1. パッケージのインストール
DNSサーバを立ち上げるために必要なパッケージ(BIND)をインストールします。
``` bash
yum -y install bind bind-chroot bind-utils
```
bind-chrootはbindを保護するchroot機能を組み込むためにインストールします。  
bind-utilsはのちの手順でdigコマンドを実行するためにインストールします。  
  
## 2. 権威DNSの設定
権威DNSサーバとは（以下、コピペ）、
『あるドメイン名の情報を記録・管理する正当な権限を有し、
そのドメインの情報についての外部からの問い合わせに応答するDNSサーバ』のこと。  
で、設定ファイルであるnamed.confやゾーンファイルの設定をするのですが、
以下のサイトがわかりやすく書いてあったので、ここではサイトを紹介するだけに留めておきます。  
  
[権威DNSサーバーにおける設定の基本を教えてください（BIND編）](http://www.atmarkit.co.jp/ait/articles/1502/10/news010.html "権威DNSサーバーにおける設定の基本を教えてください（BIND編）")

## 3. iptablesの設定
DNSサーバの通知を有効にするために、以下のようにコマンドを入力し、ポートを解放します。  

``` bash
iptables -A INPUT -p tcp -m tcp --dport 53 -j ACCEPT
iptables -A INPUT -p udp -m udp --dport 53 -j ACCEPT
service iptables save
```
