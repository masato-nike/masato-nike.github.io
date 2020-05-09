---
title: "Web会議システム構築（第3回 オレオレサーバ証明書の発行～Jitsi Meetの設定）"
date: 2020-05-09T17:50:32+09:00
author: Masato Nike
comments: true
tags: ['Build Server', 'Linux', 'SSL', 'WebMeeting']
---
本稿の前提条件として、以下が実施させているものとします。

[第1回 Linux（CentOS）サーバの構築](http://blog.masato-nike.net/post/2020-05-01-web-meeting-1/ "第1回 Linux（CentOS）サーバの構築")<br />

[第2回 Linux（CentOS）へのJitsi Meetのインストール](http://blog.masato-nike.net/post/2020-05-09-JitsiMeet-on-CentOS-2/ "第2回 Linux（CentOS）へのJitsi Meetのインストール")<br />

Web会議システム『Jitsi Meet』を動作させるためには、SSLサーバ証明書が必要です。<br />
インターネット内のサーバであれば、『[Let's Encrypt](https://letsencrypt.org/ja/ "Let's Encrypt")』といった無料のSSLサーバ証明書が使えるのですが、今回はイントラネット内で利用するということが前提ですので、『Let's Encrypt』は使えません。<br />
そこで、OpenSSLを使ったオレオレサーバ証明書が必要になります。<br />
<!--more-->
## 1. SSL証明書の発行
(1) Jitsi Meetをインストールした仮想Linuxサーバにrootでログインし、以下のコマンドを実行してください。
``` bash
mkdir /etc/ssl/work
cd ~
mkdir work
cd work
vim subjectnames.txt
```
(2) subjectnames.txtの内容は以下を入力してください。
``` bash
subjectAltName = DNS:<<host名.ドメイン名>>, IP:192.168.100.10
```
(3) 以下のコマンドを入力してください。
``` bash
openssl genrsa 2048 > server.key
openssl req -new -key server.key -subj "/C=JP/ST=Some-State/O=Some-Org/CN=<<host名.ドメイン名>>" > server.csr
openssl x509 -days 3650 -req -extfile subjectnames.txt -signkey server.key < server.csr > server.crt
server.crt
```
(4) server.crtの中身をコピーし、ローカルパソコン内に保存してください（ファイル名：server.crt）。<br />
<br />
※オレオレサーバ証明書のクライアント（Google Chrome）へのインストール方法についてはUbuntuの時に書いた以下を参照ください。<br />
[第3回 オレオレサーバ証明書の発行～クライアントへの証明書のインストール](http://blog.masato-nike.net/post/2020-05-01-web-meeting-3/ "第3回 オレオレサーバ証明書の発行～クライアントへの証明書のインストール")<br />
<br />
(5) 以下のコマンドを入力してください。
``` bash
mv server.* /etc/ssl/work/
```
<br />
## 2. Jit Meetの設定と起動
(1) 以下のコマンドを入力してください。
``` bash
cp /etc/ssl/work/server.* ~/.jitsi-meet-cfg/web/nginx/keys/
vim ~/.jitsi-meet-cfg/web/nginx/ssl.conf
```
【編集内容】
``` bash
ssl_certificate /config/keys/server.crt;
ssl_certificate_key /config/keys/server.key;
```
(2) 以下のコマンドを入力してください。
``` bash
chcon system_u:object_r:httpd_config_t:s0 /etc/ssl/work/server.crt
chcon system_u:object_r:httpd_config_t:s0 /etc/ssl/work/server.key
cd ~/docker-jitsi-meet/
docker-compose up -D
```
以上でJit Meetが起動しているはずです。<br />
SSLサーバ証明書をインストールしたGoogleChromeでサーバにアクセスしてください。
