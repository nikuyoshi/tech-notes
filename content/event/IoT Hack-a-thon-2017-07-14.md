+++
title = "IoT Hack-a-thon 2017-07-14"
+++

日時: 2017-07-14

AWS EC2インスタンス
T2.micro
ストレージ 10GB

## LINE Developer

* Bot登録をしてアクセストークン発行
  + https://developers.line.me/web-api/channel-registration
* Botの登録方法
  + https://developers.line.me/line-login/overview
* Line APIを簡単に使えるようにするため、以下の依存関係を追加
  + line-bot-spring-boot
    - https://github.com/line/line-bot-sdk-java/

* LINE Notifyでメッセージ送信する

## Java監視

* ファイル監視
https://docs.oracle.com/cd/E26537_01/tutorial/essential/io/notification.html

**WatchKeyをリセットしないとReadyステータスにならないため、永遠にファイルを読み込まない!!**


