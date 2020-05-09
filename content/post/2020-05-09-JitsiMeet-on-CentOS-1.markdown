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
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_015.JPG)<br /><br />
(8) 作成した仮想マシンを選択し、設定(S)をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0025.JPG) <br /><br />
(9) [ネットワーク]を選択し、割り当て(A)を"ブリッジアダプター"にしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0026.JPG) <br /><br />
(10) [システム]を選択し、"ハードディスク"と"光学"を入れ替えてください。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_000.JPG)<br /><br />
<br />
## 4. CentOSのインストール
(1) [起動(T)]をクリックし、作成した仮想マシンを起動させてください。<br />
(2) [追加(A)]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting1/WebMeet1_0027.JPG) <br /><br />
(3) ダウンロードしたCentOSのISOイメージを選択し、[選択]をクリックしてください。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_016.JPG)<br /><br />
(4) [起動]をクリックしてください。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_017.JPG)<br /><br />
(5) CentOSが起動したら、[Enter]キーを押してください。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_001.JPG)<br /><br />
(6) "日本語"を選択し、[続行]ボタンをクリックしてください。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_002.JPG)<br /><br />
(7) 以下の画面で様々なインストールの設定を行います。まずは[システム]の[インス（トール先）]をクリックしてください。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_003.JPG)<br /><br />
(8) [ローカルの標準ディスク]にて、作成した"HARDDISK"をクリックし、[完了]ボタンを押してください。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_004.JPG)<br /><br />
(9) 次に[ソフトウェアの選択]をクリックしてください。<br /><br />
(10) 左の一覧（ベース環境）から"サーバー"を選択し、その他のソフトウェアで"開発ツール"を選択し、[完了]ボタンを押してください。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_005.JPG)<br /><br />
(11) 次に[ネット（ワークとホスト名）]をクリックしてください。<br /><br />
(12) ホスト名にフルコンピュータ名を入力し、[適用]ボタンをクリックしてください。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_006.JPG)<br /><br />
(13) [設定]ボタンをクリックしてください。<br /><br />
(14) [IPv4設定]タグにてIPアドレスなどネットワーク情報を入力し、[保存]ボタンをクリックしてください。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_007.JPG)<br /><br />
(15) [Ethernet]を"オン"にし、[完了]ボタンを押してください。<br /><br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_008.JPG)<br /><br />
(16) (7)の画面で[時刻と日付]をクリックしてください。<br /><br />
(17) "ntp.jst.mfeed.ad.jp"を追加し、[OK]ボタンをクリックしてください。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_009.JPG)<br /><br />
(19) [地域]にて"アジア"を、[都市]にて"東京"を選択し、[完了]ボタンをクリックしてください。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_010.JPG)<br /><br />
(20) (7)の画面で[インストールの開（始）]をクリックしてください。<br /><br />
(21) インストールが開始されます。その間にrootのパスワードを決めます。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_011.JPG)<br /><br />
(22) rootのパスワードを入力し、[完了]ボタンを押してください。<br /><br />
(23) 次にユーザーの作成を行います。ログインID、パスワードなどのユーザー情報を入力し、[完了]ボタンを押してください。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_012.JPG)<br /><br />
(24) インストールが完了したら、[再起動]ボタンを押してください。<br />
![Web会議システム構築](/images/blog/JitsiMeetonCentOS1/InstallCentOS_013.JPG)<br /><br />
<br />
以上でLinuxサーバの構築は終了です。

