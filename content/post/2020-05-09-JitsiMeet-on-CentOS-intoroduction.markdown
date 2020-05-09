---
title: "CentOSへのJitsi Meetのインストール（序章 コロナに負けるな！）"
date: 2020-05-09T12:08:20+09:00
author: Masato Nike
comments: true
tags: ['COVID-19', 'Build Server', 'Linux', 'WebMeeting', 'SSL', 'WebMeeting']
---
UbuntuへのオープンソースのWeb会議システム『Jitsi Meet』のインストールを紹介してきましたが、CentOSでできないものかと調べてみたので書いておく。<br />
CentOSへの『Jitsi Meet』の対応はRPMが2017年2月7日以降更新されていない状況です(2020年5月9日現在)。<br />
なので、セキュリティとかバグとかもろもろの観点から、CentOSへの『Jitsi Meet』のインストールはあまりお勧めできません<br />
それでも、もろもろの事情でCentOSを利用しなきゃならないこともあると思うので、3回に分けて記述していきたいと思います。<br />
<br />
<!--more-->
[第1回 Linux（CentOS）サーバの構築](http://blog.masato-nike.net/post/2020-05-09-JitsiMeet-on-CentOS-1/ "第1回 Linux（CentOS）サーバの構築")<br />

[第2回 Linux（CentOS）へのJitsi Meetのインストール](http://blog.masato-nike.net/post/2020-05-09-JitsiMeet-on-CentOS-2/ "第2回 Linux（CentOS）へのJitsi Meetのインストール")<br />

[第3回 オレオレサーバ証明書の発行～Jitsi Meetの設定](http://blog.masato-nike.net/post/2020-05-09-JitsiMeet-on-CentOS-3/ "第3回 オレオレサーバ証明書の発行～Jitsi Meetの設定")<br />
<br />
なお、オレオレサーバ証明書のクライアント（Google Chrome）へのインストール方法についてはUbuntuの時に書いた以下を参照ください。<br />
<br />
[第3回 オレオレサーバ証明書の発行～クライアントへの証明書のインストール](http://blog.masato-nike.net/post/2020-05-01-web-meeting-3/ "第3回 オレオレサーバ証明書の発行～クライアントへの証明書のインストール")<br />
