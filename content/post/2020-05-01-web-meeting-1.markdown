---
title: "Web会議システム構築（第1回 Linux（Ubuntu）サーバの構築）"
date: 2020-05-01T16:27:29+09:00
author: Masato Nike
comments: true
tags: ['Build Server', 'Linux', 'WebMeeting']
---
Web会議システムをイントラネット内に構築する方法として、仮想Linuxサーバを構築し、そこに『Jitsi Meet』をインストールする方法が考えられます。<br />

以下のソフトウェアをWindows10にインストールしました（2020年4月30日現在最新？）<br />

|ソフトウェア|バージョン|入手先|
|:--|:--:|--:|
|VirtualBox|6.1.6-137129|[Downloads – Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads "Downloads – Oracle VM VirtualBox")|
|Ubuntu|20.04|[Ubuntuを入手する](https://jp.ubuntu.com/download "Ubuntuを入手する")|

それぞれ自分の環境にあったものをダウンロードしてください。<br />
<!--more-->
## 1. VirtualBoxのインストール
(1) [Next]をクリック。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0012.JPG) <br /><br />
(2) [Next]をクリック。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0013.JPG) <br /><br />
(3) [Next]をクリック。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0014.JPG) <br /><br />
(4) [Yes]をクリック。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0015.JPG) <br /><br />
(5) [Install]をクリック。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0016.JPG) <br /><br />
(6) [Finish]をクリック。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0017.JPG) <br /><br />
<br />
<br />
## 2. BIOSの変更
(1) BIOSにて仮想化機能を有効にする必要があるため、パソコンを再起動させてください。<br /><br />
(2) BIOSにて仮想化機能を有効にしてください。<br />
　　※仮想化機能の有効化については、マザーボードメーカーによって異なります。<br />
　　　Googleなどで『BIOS virtualization <メーカー名>』で検索してみてください。<br />
<br />
## 3. Ubuntuのインストール前の準備
(1) VirtualBoxを起動し、[仮想マシン(M)]-[新規(N)]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0018.JPG) <br /><br />
(2) 仮想マシンを作成します。名前やフォルダーを適宜変更して、[次へ]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0019.JPG) <br /><br />
(3) メモリーサイズを変更して、[次へ]をクリックしてください（私は搭載メモリの半分を割り当てました）。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0020.JPG) <br /><br />
(4) そのまま[作成]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0021.JPG) <br /><br />
(5) そのまま[次へ]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0022.JPG) <br /><br />
(6) そのまま[次へ]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0023.JPG) <br /><br />
(7) そのまま[作成]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0024.JPG) <br /><br />
(8) 作成した仮想マシンを選択し、設定(S)をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0025.JPG) <br /><br />
(9) [ネットワーク]を選択し、割り当て(A)を"ブリッジアダプター"にしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0026.JPG) <br /><br />
<br />
## 4. Ubuntuのインストール
(1) [起動(T)]をクリックし、作成した仮想マシンを起動させてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0027.JPG) <br /><br />
(2) [追加(A)]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0027.JPG) <br /><br />
(3) ダウンロードしたUbuntuのISOイメージを選択し、[選択]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0028.JPG) <br /><br />
(4) [起動]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0029.JPG) <br /><br />
(5) 左の言語リストから"日本語"を選択し、[Ubuntuをインストール]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0030.JPG) <br /><br />
(6) [続ける]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0032.JPG) <br /><br />
(7) [続ける]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0034.JPG) <br /><br />
(8) [インストール]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0036.JPG) <br /><br />
(9) [続ける]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0037.JPG) <br /><br />
(10) [続ける]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0038.JPG) <br /><br />
(11) [あなたの名前]（ユーザ名）などを入力し、[続ける]をクリックしてください。<br />
　　※コンピュータ名はDNSに登録されている必要があります。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0039.JPG) <br /><br />
これでインストールが開始されます。しばらくお待ちください。<br /><br />
(12) インストールが終了すると再起動を求められるので、[今すぐ再起動する]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0040.JPG) <br /><br />
(13) [Enter]キーを押してください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0041.JPG) <br /><br />
(14) 再起動後、以下のような画面になります。[スキップ(S)]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0000.JPG) <br /><br />
(15) [次へ(N)]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0001.JPG) <br /><br />
(16) [次へ(N)]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0002.JPG) <br /><br />
(17) [次へ(N)]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0003.JPG) <br /><br />
(18) [完了(D)]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0004.JPG) <br /><br />
(19) 以下のダイアログが表示されたら、[今すぐインストールする)]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0005.JPG) <br /><br />
(20) ネットワークの設定を行います。[有線設定]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0006.JPG) <br /><br />
(21) 歯車マークをクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0007.JPG) <br /><br />
(22) IPv4メソッドを[手動]にし、IPアドレス、DNSなどの情報を入力してください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0008.JPG) <br /><br />
(23) 設定を反映させるために、一度再起動させます。[電源オフ]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0009.JPG) <br /><br />
(24) [再起動]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0010.JPG) <br /><br />
<br />
以上でLinuxサーバの構築は終了です。
