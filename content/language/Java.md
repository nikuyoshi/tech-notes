+++
title = "Java"
+++

## Permanent(Metaspace)領域、C領域の調査について

Javaのツールだと確認ができないため、以下のようにコアから判断する。
なお、以下のコマンドはざっくりと判断するためのもので、きちんと確認をしたいのであればコアを解析するツールを使うべきである。

```sh
指定プロセスのコアを取得するため、HDDの空き容量を十分に確保しておく。CCM Agentであれば1GB近く。
gcore -o ${ファイル名} ${PID} 
strings -a ${ファイル名} > ${一時ファイル}
sort ${一時ファイル} | uniq -c | sort -nr | less
```

## WireMock

* 公式ドキュメント http://wiremock.org/docs/ の各項目をざっと読む
* 以下のようなJSON形式ファイルを準備しておくと、 `http:localhost:8080/api/mytest` のようなAPIが自動生成される。

```text
{
    "request": {
        "method": "GET",
        "url": "/api/mytest"
    },
    "response": {
        "status": 200,
        "body": "More content\n"
    }
}
```

* プロキシ機能もあり、http://search.twitter.com のURLをバインドさせて、`curl "http://localhost:8080/search.json?q=from:sirbonar&result_type=recent&rpp=1"`  のようにローカルに向けてAPIを実行するとその実行結果の結果を記録してくれる。 結果がJSON形式で残るため、再度同じリクエストを送ることも可能。

### フォルダ構成

```text
├── mappings 
│   └── test.json ← モック生成用JSON
└── wiremock-standalone-2.7.1.jar ←実行ライブラリ
```

### 起動方法

* オプション無し

```bash
java -jar wiremock-standalone-2.7.1.jar
```

* Record and Playback(New)
  + 管理画面からTarget URLを設定する新方式

```bash
java -jar wiremock-standalone-2.7.1.jar --enable-browser-proxying
```

* Record and Playback (Legacy)
 
```bash
java -jar wiremock-standalone-2.7.1.jar --proxy-all="http://search.twitter.com" --record-mappings --verbose
```


## Spring

### Daemon化

https://docs.spring.io/spring-boot/docs/current/reference/html/deployment-install.html

ex: `java -jar ../lib/notifier-0.0.1-SNAPSHOT.jar -Dlogback.configurationFile=../conf/logback.xm`

### 設定ファイルの読み込み

https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html

