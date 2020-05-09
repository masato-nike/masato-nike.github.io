---
title: "Web会議システム構築（第2回 Linux（CentOS）へのJitsi Meetのインストール）"
date: 2020-05-09T16:57:56+09:00
author: Masato Nike
comments: true
tags: ['Build Server', 'Linux', 'WebMeeting']
---
Linux(CentOS)にWeb会議システム『Jitsi Meet』をインストールします。<br />
前提として、以下を実施しているものとします。<br />
<br />
[第1回 Linux（CentOS）サーバの構築](http://blog.masato-nike.net/post/2020-05-09-jitsimeet-on-centos-1/ "第1回 Linux（CentOS）サーバの構築")<br />
<!--more-->
## 1. SSHの設定
(1) rootでログインし、以下のコマンドを入力してください。<br />

``` bash
firewall-cmd --add-service ssh --permanent
```
(2) rootでのログインを拒否するように設定します。<br />
<br />
【コマンド】
``` bash
vim /etc/ssh/sshd_config
```
【編集内容】
```
PermitRootLogin no
```
<br />
(3) 以下のコマンドを入力してください。<br />
``` bash
systemctl restart sshd
systemctl status sshd
```
以上で、SSHの設定は終了です。<br />
<br />
## 2. Dockerのインストール
(1) rootでログインし、以下のコマンドを入力してください。<br />

``` bash
dnf -y remove podman
dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
dnf -y install --nobest docker-ce docker-ce-cli
dnf -y update https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.2.13-3.1.el7.x86_64.rpm
dnf -y update docker-ce
systemctl enable docker
systemctl start docker
docker version
dnf upgrade
firewall-cmd --add-service http --permanent
firewall-cmd --add-service https --permanent
firewall-cmd --add-port 10000-20000/udp --permanent
firewall-cmd --add-masquerade --permanent
firewall-cmd --reload
```
<br />
## 3. Docker Composeのインストール
(1) rootでログインし、以下のコマンドを入力してください。<br />
``` bash
dnf -y install jq
vim docker-compose-install.sh
``` 
【編集内容】
``` bash
compose_version=$(curl https://api.github.com/repos/docker/compose/releases/latest | jq .name -r)
output='/usr/local/bin/docker-compose'
curl -L https://github.com/docker/compose/releases/download/$compose_version/docker-compose-$(uname -s)-$(uname -m) -o $output
chmod +x $output
$output --version
```
(2) 以下のコマンドを入力してください。<br />
``` bash
chmod +x docker-compose-install.sh
./docker-compose-install.sh
```
<br />
## 4. Jitsi Meetのインストール
(1) rootでログインし、以下のコマンドを入力してください。<br />
``` bash
git clone https://github.com/jitsi/docker-jitsi-meet && cd docker-jitsi-meet
cp env.example .env
vim .env
```
【編集内容】
``` bash
CONFIG=/root/.jitsi-meet-cfg

HTTP_PORT=80

HTTPS_PORT=443

TZ=Asia/Tokyo

PUBLIC_URL=https://hostname.yourdomain

ENABLE_LETSENCRYPT=0
```
(2) 以下のコマンドを入力してください。<br />
``` bash
./gen-passwords.sh
mkdir -p ~/.jitsi-meet-cfg/{web/letsencrypt,transcripts,prosody,jicofo,jvb}
docker-compose pull
docker-compose up -d
docker-compose down
```
以上で、『Jitsi Meet』のインストールは終了ですが、まだ起動はできません。<br />
httpsでアクセスするため、SSLサーバ証明書の設定が必要になります。<br />
SSLサーバ証明書の設定は以下に続きます。<br />
<br />
[第3回 オレオレサーバ証明書の発行～Jitsi Meetの設定](http://blog.masato-nike.net/post/2020-05-09-jitsimeet-on-centos-3/ "第3回 オレオレサーバ証明書の発行～Jitsi Meetの設定")<br />
