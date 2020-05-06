---
title: Web会議システム構築（第4回 スマホのカメラでWeb会議）
date: 2020-05-01T19:11:24+09:00
author: Masato Nike
comments: true
tags: ['iPhone', 'Android', 'SmartPhoneAppli', 'WebMeeting']
---
2020年5月1日現在、新型コロナウイルスの影響で、テレワークによる作業が多くなっているせいか、Webカメラが品薄状態となっています。<br />
Webカメラがないのでは、せっかく『Jitsi Meet』でWebシステムを構築したとしても使い物になりません。<br />
そこで注目したのがスマートフォンに搭載されているカメラをWebカメラの代わりにできないかということです。<br />
<!--more-->
## 1. iVCam
インストールは簡単なので、とりあえず、リンクだけ貼っておきます。<br />
<br />
[スマホ（Android）のカメラをWebカメラにするアプリ](https://play.google.com/store/apps/details?id=com.e2esoft.ivcam&hl=ja "スマホ（Android）のカメラをWebカメラにするアプリ")<br />
<br />
[スマホ（iPhone）のカメラをWebカメラにするアプリ](https://apps.apple.com/jp/app/ivcam-%E3%82%B3%E3%83%B3%E3%83%94%E3%83%A5%E3%83%BC%E3%82%BF%E3%82%AB%E3%83%A1%E3%83%A9/id1164464478 "スマホ（iPhone）のカメラをWebカメラにするアプリ")<br />
<br />
[スマホのカメラをパソコンで認識させるソフト](https://www.e2esoft.com/ivcam/ "スマホのカメラをパソコンで認識させるソフト")<br />
これらをインストールしたら、同一ネットワーク（Wi-Fi環境）にてパソコン・スマホの両方でiVCamを実行するか、もしくは、USBケーブルでスマホとパソコンを接続し、実行してください。<br />

# 2. 仮想サウンドカード
私のパソコン環境では市販のサウンドカードを増設してあるので、マイクはLineInで平気だったのですが、サウンドカードを増設していない人は仮想サウンドカードというのが必要みたいです。<br />
ここでは無料の仮想サウンドカードとして、『[VB-CABLE](https://www.vb-audio.com/Cable/index.htm "VB-CABLE")』を紹介します。<br />
<br />
(1) 以下のURLのDownloadをクリックし、VB-CABLE Driverをダウンロードしてください。<br />
<br />
[https://www.vb-audio.com/Cable/index.htm](https://www.vb-audio.com/Cable/index.htm "https://www.vb-audio.com/Cable/index.htm")<br />
<br />
(2) ダウンロードしたファイルを解凍し、VBCABLE_Setup_x64.exe（もしくは、VBCABLE_Setup.exe）を右クリックして、[管理者として実行]をクリックしてください。<br />
<br />
(3) [Install]をクリックしてください。<br />
<br />
次に、Windowsのサウンドの設定です。<br />
(4) [スタートメニュー]－[設定]より、[システム]をクリックしてください。<br />
![Web会議システム構築](/images/blog/WebMeeting4/WebMeet4_001.JPG) <br /><br />
(5) [サウンド]を選択し、出力を"スピーカー"、入力を"CABLE Putput (VB-Audio Virtual Cable)"に設定してください。<br />
![Web会議システム構築](/images/blog/WebMeeting4/WebMeet4_002.JPG) <br /><br />
<br />
以上で設定は終わりです。Jitsi Meetサーバに接続し、相手に音声が伝わることを確認してください。
