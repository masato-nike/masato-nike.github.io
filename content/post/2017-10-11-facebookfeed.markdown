---
layout: post
title: "FacebookのRSSを取得する（永久ページアクセストークンの取得）"
date: 2017-10-11 06:35:53 +0900
comments: true
tags: ['MakeupHomePage', 'Facebook']
---
FacebookのRSSを取得し、自分のホームページのTOPICSにしたいなぁと考えた次第です。<br />
FacebookのRSSを取得するには、ページアクセストークンなるものが必要なのですが、通常の方法だと、有効期限が1時間以内のアクセストークンが取得できません。<br />
それだといくらRSSを取得できても、ホームページのTOPICSに使用するには有効期限が短すぎます。
そこで、永久的なアクセストークンを取得できないかと、いろいろぐぐってみたわけです。<br />
<!--more-->
以下に私が調査した方法（2017年10月11日時点）を記しておきます。

##　1. （事前準備）アプリ登録およびアプリ情報の取得

Facebookにログインし、アプリ管理をクリックします。

![アプリ管理](/images/blog/2017/10/11/facebookfeed_001.jpg)

[新しいアプリを作成]ボタンをクリックしてください。

![新しいアプリを作成](/images/blog/2017/10/11/facebookfeed_002.jpg)

表示されたダイアログで、アプリの表示名を入力します。

![アプリの表示名](/images/blog/2017/10/11/facebookfeed_003.jpg)

セキュリティチェックを行い、送信ボタンをクリックします。
これでアプリが作成されるはずです。

[設定]―[ベーシック]を表示し、『アプリID』と『app secret』をメモしておいてください。

![アプリ情報](/images/blog/2017/10/11/facebookfeed_004.jpg)


## 2. ユーザアクセストークンの取得

グラフAPIエクスプローラ https://developers.facebook.com/tools/explorer/145634995501895/ にアクセスします。

アプリにて、作成したアプリを選択します。

![アプリ選択](/images/blog/2017/10/11/facebookfeed_005.jpg)


トークンを取得かから、[ユーザアクセストークンを取得]を選択します。

![ユーザアクセストークンを選択](/images/blog/2017/10/11/facebookfeed_006.jpg)


manage_pages　にチェックを入れ、アクセストークンを取得します。

![権限付与](/images/blog/2017/10/11/facebookfeed_007.jpg)


Facebookでログインダイアログが表示されるので、ログインしてください。

![ログイン認証](/images/blog/2017/10/11/facebookfeed_008.jpg)


ログインしたダイアログにアクセストークンがコールバックされるので、メモしてください（UUU1H）。

![ユーザアクセストークン](/images/blog/2017/10/11/facebookfeed_009.jpg)

<code>
https://developers.facebook.com/tools/explorer/callback#access_token=UUU1H&expires_in=5762
</code>

## 3. ユーザアクセストークンの延長

[ツール＆サポート]をクリックしてください。

![ツール＆サポート](/images/blog/2017/10/11/facebookfeed_010.jpg)

アクセストークンツールをクリックしてくだい。

![アクセストークンツール](/images/blog/2017/10/11/facebookfeed_011.jpg)

[User Token]のデバッグを実施します。

![User Token](/images/blog/2017/10/11/facebookfeed_012.jpg)

アクセストークンツールにて、アクセストークンUUU1Hをコピペし、デバッグを実施してください。

![ユーザアクセストークン](/images/blog/2017/10/11/facebookfeed_013.jpg)

アクセストークンを延長してください。

![ユーザアクセストークンの延長](/images/blog/2017/10/11/facebookfeed_014.jpg)

表示されたアクセストークンをメモしてください（UUU2M）。

## 4. 無期限ユーザアクセストークンの取得
<code>
https://graph.facebook.com/oauth/access_token?grant_type=fb_exchange_token&client_id=<アプリID>&client_secret=<app secret>&fb_exchange_token=UUU2M
</code>

にアクセスしてください。
JSONファイルがダウンロードもしくは表示されるので、保存してください。

<code>
{"access_token":"UUU8","token_type":"bearer","expires_in":5183824}
</code>

## 5. 無期限ページアクセストークンの取得
```
https://graph.facebook.com/me/accounts?access_token=UUU8
```

にアクセスしてください。
JSONファイルがダウンロードもしくは表示されるので、保存してください。

```
{
   "data": [
      {
         "access_token": "PPP8",
         "category": "Community",
         "name": "hogehoge",
         "id": "pegepge",
         "perms": [
            "ADMINISTER",
            "EDIT_PROFILE",
            "CREATE_CONTENT",
            "MODERATE_CONTENT",
            "CREATE_ADS",
            "BASIC_ADMIN"
         ]
      }
   ],
   "paging": {
      "cursors": {
         "before": "guhaguha",
         "after": "haguhagu"
      }
   }
}
```

アクセストークンデバッガーにて、上記アクセストークン（PPP8）を入力し、デバッグを実行してください。
有効期限が受け取らないになっていることを確認してください。

![無期限ページアクセストークン](/images/blog/2017/10/11/facebookfeed_015.jpg)

## 6. FacebookページのRSSを取得

Facebookページの[ページ情報]に記されている『ページID』をメモしてください。
ブラウザやJavascriptを用い、以下のアドレスにアクセスするとFacebookページのRSSが取得できます。

```
https://graph.facebook.com/v2.10/<ページID>/feed?fields=created_time%2Cmessage&access_token=PPP8
```
