---
title: "Web会議システム構築（第1回 Linux（CentOS）サーバの構築）"
date: 2020-05-09T12:47:20+09:00
author: Masato Nike
comments: true
tags: ['Build Server', 'Linux', 'WebMeeting']
---
以下のソフトウェアをWindows10にインストールしました（2020年4月30日現在最新？）<br />

|ソフトウェア|バージョン|入手先|
|:--|:--:|--:|
|VirtualBox|6.1.6-137129|[Downloads – Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads "Downloads – Oracle VM VirtualBox")|
|CentOS|8.1.1911|[Download CentOS](https://www.centos.org/download/ "Download CentOS")|

それぞれ自分の環境にあったものをダウンロードしてください。<br />
<!--more-->
## 1. VirtualBoxのインストール
以下を参照してください。<br />
<br />
[第1回 Linux（Ubuntu）サーバの構築](http://blog.masato-nike.net/post/2020-05-01-web-meeting-1/ "第1回 Linux（Ubuntu）サーバの構築")<br />
<br />
## 2. BIOSの変更
(1) BIOSにて仮想化機能を有効にする必要があるため、パソコンを再起動させてください。<br /><br />
(2) BIOSにて仮想化機能を有効にしてください。<br />
　　※仮想化機能の有効化については、マザーボードメーカーによって異なります。<br />
　　　Googleなどで『BIOS virtualization <メーカー名>』で検索してみてください。<br />
<br />
## 3. CentOSのインストール前の準備
(1) VirtualBoxを起動し、[仮想マシン(M)]-[新規(N)]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0018.JPG) <br /><br />
(2) 仮想マシンを作成します。名前やフォルダーを適宜変更して、[次へ]をクリックしてください。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_014.JPG) <br /><br />
(3) メモリーサイズを変更して、[次へ]をクリックしてください（私は搭載メモリの半分を割り当てました）。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0020.JPG) <br /><br />
(4) そのまま[作成]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0021.JPG) <br /><br />
(5) そのまま[次へ]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0022.JPG) <br /><br />
(6) そのまま[次へ]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0023.JPG) <br /><br />
(7) 20GB程度を指定し、[作成]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0024.JPG) <br /><br />
(8) 作成した仮想マシンを選択し、設定(S)をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0025.JPG) <br /><br />
(9) [ネットワーク]を選択し、割り当て(A)を"ブリッジアダプター"にしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0026.JPG) <br /><br />
(10) [システム]を選択し、"ハードディスク"と"光学"を入れ替えてください。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_000.JPG)<br /><br />
<br />
## 4. CentOSのインストール
これから書きます。。。
