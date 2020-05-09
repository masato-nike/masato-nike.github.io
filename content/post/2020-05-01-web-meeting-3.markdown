---
title: "Web会議システム構築（第3回 オレオレサーバ証明書の発行～クライアントへの証明書のインストール）"
date: 2020-05-01T19:07:06+09:00
author: Masato Nike
comments: true
tags: ['Build Server', 'Linux', 'SSL', 'WebMeeting']
---
本稿の前提条件として、以下が実施させているものとします。

[第1回 Linux（Ubuntu）サーバの構築](http://blog.masato-nike.net/post/2020-05-09-JitsiMeet-on-CentOS-1/ "第1回 Linux（Ubuntu）サーバの構築")<br />

[第2回 Linux（Ubuntu）へのJitsi Meetのインストール](http://blog.masato-nike.net/post/2020-05-01-web-meeting-2/ "第2回 Linux（Ubuntu）へのJitsi Meetのインストール")<br />

Web会議システム『Jitsi Meet』を動作させるためには、SSLサーバ証明書が必要です。<br />
インターネット内のサーバであれば、『[Let's Encrypt](https://letsencrypt.org/ja/ "Let's Encrypt")』といった無料のSSLサーバ証明書が使えるのですが、今回はイントラネット内で利用するということが前提ですので、『Let's Encrypt』は使えません。<br />
そこで、OpenSSLを使ったオレオレサーバ証明書が必要になります。<br />
<!--more-->
## 1. SSL証明書の発行
(1) Jitsi Meetをインストールした仮想Linuxサーバにログインし、以下のコマンドを実行してください。
``` bash
sudo mkdir /etc/ssl/work
cd ~
mkdir work
cd work
vi subjectnames.txt
```
(2) subjectnames.txtの内容は以下を入力してください。
``` bash
subjectAltName = DNS:<<host名.ドメイン名>>, IP:192.168.100.10
```

(3) 以下のコマンドを入力してください。
``` bash
sudo openssl genrsa 2048 > server.key
sudo openssl req -new -key server.key -subj "/C=JP/ST=Some-State/O=Some-Org/CN=<<host名.ドメイン名>>" > server.csr
sudo openssl x509 -days 3650 -req -extfile subjectnames.txt -signkey server.key < server.csr > server.crt
more server.crt
```
(4) server.crtの中身をコピーし、ローカルパソコン内に保存してください（ファイル名：server.crt）。<br />
<br />

## 2. クライアントへの証明書のインストール
(1) ローカルパソコンにて、Google Chromeを起動してください。<br />
　　※Google Chrimeがインストールされていない場合は、インストールしてください。<br />
(2) 右上のメニューから[設定]をクリックしてください。
![Web会議システム構築](/images/blog/WebMeeting3/WebMeeting3_0000.JPG) <br /><br />
(3)[プライバシーとセキュリティ]をクリックしてください。
![Web会議システム構築](/images/blog/WebMeeting3/WebMeeting3_0001.JPG) <br /><br />
(4) [もっと見る]をクリックし、[証明書の管理]をクリックしてください。
![Web会議システム構築](/images/blog/WebMeeting3/WebMeeting3_0002.JPG) <br /><br />
(5) [信頼されたルート証明機関]をクリックし、[インポート]をクリックしてください。
![Web会議システム構築](/images/blog/WebMeeting3/WebMeeting3_0003.JPG) <br /><br />
(6) [次へ]をクリックしてください。
![Web会議システム構築](/images/blog/WebMeeting3/WebMeeting3_0004.JPG) <br /><br />
(7) [参照]を押し、ローカルパソコンに保存した"server.crt"を選択後、[次へ]をクリックしてください。
![Web会議システム構築](/images/blog/WebMeeting3/WebMeeting3_0005.JPG) <br /><br />
(8) [信頼されたルート証明機関]であることを確認し、[次へ]をクリックしてください。
![Web会議システム構築](/images/blog/WebMeeting3/WebMeeting3_0006.JPG) <br /><br />
(9) [完了]をクリックしてください。
![Web会議システム構築](/images/blog/WebMeeting3/WebMeeting3_0007.JPG) <br /><br />
(10) [はい(Y)]をクリックしてください。
![Web会議システム構築](/images/blog/WebMeeting3/WebMeeting3_0008.JPG) <br /><br />
<br />
この作業は本システムを利用するすべてのパソコンで行ってください。<br />
<br />
## 3. Jit Meetの設定と起動
(1) 以下のコマンドを実行してください。
``` bash
sudo mv server.* /etc/ssl/work
sudo vi /etc/nginx/sites-enabled/<<host名.ドメイン名>>.conf
```
(2) <<host名.ドメイン名>>.confの以下のように修正してください。
``` bash
ssl_certificate /etc/ssl/work/server.crt;
ssl_certificate_key /etc/ssl/work/server.key;
```
(3) 以下のコマンドを実行してください。
``` bash
sudo systemctl restart nginx
sudo systemctl status nginx
```
以上でJit Meetが起動しているはずです。<br />
SSLサーバ証明書をインストールしたGoogleChromeでサーバにアクセスしてください。
