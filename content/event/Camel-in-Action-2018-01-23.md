---
title: "第5回Camel In Action 読書会＠恵比寿"
date: 2017-12-19T19:21:18+09:00
draft: false
---

### 2.6.2 - 2.7

カスタムプロセッサを自作できるが、`setBody`などを設定できるが見えにくくなるためやめたほうが良いとのこと。

### 3.2

Componentにhttpを使用すると、ApacheのHTTP Clientを使うため、HTTPの受け口を開けるなら、JettyやUndertowを使えば良いらしい。
transformは手元のメッセージを変換する。 enrich, pollEnrichはリモートのメッセージを取得してごにょごにょするらしい。
前の情報を意図的に覚えておいて、情報を操作する場合にenrichを使えば良いのでは、との話が挙がった。
