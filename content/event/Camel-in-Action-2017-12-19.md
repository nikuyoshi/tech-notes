---
title: "第４回Camel In Action 読書会＠恵比寿"
date: 2017-12-19T19:21:18+09:00
draft: true
---

[イベントページ](https://jcug-oss.connpass.com/event/72970/)

## @tadayosiさんによるプレゼン

[資料](https://tadayosi.github.io/jjug2017-camel_hawtio_springboot/reveal.js/index.html#/agenda-1)

* Circuit Breakerパターン
  * マイクロサービスで協調して動作する際に、お互いとも倒れしないようにするアーキテクチャ

## Chapter 2.5

* エンドポイントをExchangeの内容に応じて動的に変更できる。 Simple構文を覚えることが大事。
* URIで特殊な文字を使用するには、文字をraw()で囲う。
* エンドポイントを動的に変更するには、toD, xpathを使用する。
* `toD`処理は重いのでは？
  * そこまで重い処理ではないであろうとのこと。
* `${{}}`はSpringが解釈していて、`{{}}`はCamelが解釈している。 Camel in Actionは`{{}}`推し
