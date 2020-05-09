---
title: "Web会議システム構築（第2回 Linux（Ubuntu）へのJitsi Meetのインストール）"
date: 2020-05-01T19:04:09+09:00
author: Masato Nike
comments: true
tags: ['Build Server', 'Linux', 'WebMeeting']
---
Linux(Ubuntu)にWeb会議システム『Jitsi Meet』をインストールします。<br />
前提として、以下を実施しているものとします。<br />
<br />
[第1回 Linux（Ubuntu）サーバの構築](http://blog.masato-nike.net/post/2020-05-01-web-meeting-1/ "第1回 Linux（Ubuntu）サーバの構築")<br />
<!--more-->
## 1. SSHの設定
(1) アプリケーションの一覧を表示してください。
![Web会議システム構築](/images/blog/WebMeeting2/WebMeet2_0000.JPG) <br /><br />
(2) [端末]をクリックさせてください。
![Web会議システム構築](/images/blog/WebMeeting2/WebMeet2_0001.JPG) <br /><br />
<br />
以下、端末にコマンドを入力することになります。<br />
<br />
(3) SSHを利用できるようにします。以下のコマンドを入力してください。<br />

``` bash
sudo apt update
sudo apt upgrade
sudo apt install openssh-server
sudo /etc/init.d/ssh restart
sudo ufw status
sudo ufw allow proto tcp from 192.168.100.0/24 to any port 22
sudo ufw enable
```
(4) rootでのログインを拒否するように設定します。<br />
<br />
【コマンド】
``` bash
sudo vi /etc/ssh/sshd_config
```
【編集内容】
```
PermitRootLogin no
```
<br />
(5) 以下のコマンドを入力してください。<br />
``` bash
sudo systemctl restart sshd
sudo systemctl status sshd
```
以上で、SSHの設定は終了です。<br />
<br />
以下は端末で操作してもよいですし、TeraTermProなどで操作しても構いません。<br />
## 2. Jitsi Meetインストール事前準備
(1) 以下のコマンドを入力してください。<br />
``` bash
sudo ufw allow in 443/tcp
sudo ufw allow in 10000:20000/udp
sudo ufw status
sudo wget https://download.jitsi.org/jitsi-key.gpg.key
sudo apt-key add jitsi-key.gpg.key
sudo sh -c "echo 'deb https://download.jitsi.org stable/' >> /etc/apt/sources.list.d/jitsi-stable.list"
sudo apt update
sudo apt install openjdk-8-jre-headless
sudo apt install nginx
```
## 3. Jitsi Meetのインストール
(1) 以下のコマンドを入力してください。<br />
``` bash
sudo apt install jitsi-meet
```
(2) インスト―ルの途中で以下の画面になったら、<<ホスト名.ドメイン名>>を入力してください。<br />
![Web会議システム構築](/images/blog/WebMeeting2/WebMeet2_0002.JPG) <br /><br />
(2) インスト―ルの途中で以下の画面になったら、2つ目の方を選択してください。<br />
![Web会議システム構築](/images/blog/WebMeeting2/WebMeet2_0003.JPG) <br /><br />
以上で、『Jitsi Meet』のインストールは終了ですが、まだ起動はできません。<br />
httpsでアクセスするため、SSLサーバ証明書の設定が必要になります。<br />
SSLサーバ証明書の設定は以下に続きます。<br />
<br />
[第3回 オレオレサーバ証明書の発行～クライアントへの証明書のインストール](http://blog.masato-nike.net/post/2020-05-01-web-meeting-3/ "第3回 オレオレサーバ証明書の発行～クライアントへの証明書のインストール")<br />