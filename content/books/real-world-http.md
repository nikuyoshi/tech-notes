+++
title = "Real World HTTP"
draft = true
+++

## 概要

* パタヘネ本のHTTP版
* 一度でもウェブ技術に触れたことのある人が知識の整理のために読む本
* 適宜絵、スクリーンショット、表形式が挿入されており理解を促してくれている

## 読み終わることで得られるスキル

* curlの基礎知識。 代表的なオプションの意味を理解できる。
  + ex. `curl --http1.0 -F title="The Art of Community" -F author="Jono Bacon" -F attachmen-file=@_vimrc http://localhost:18888`
* Goの基礎知識。 特にHTTP周り。
  
```
package main

import (
	"fmt"
	"log"
	"net/http"
	"net/http/httputil"
)

func handler(w http.ResponseWriter, r *http.Request){
	dump, err := httputil.DumpRequest(r, true)
	if err != nil {
		http.Error(w, fmt.Sprint(err), http.StatusInternalServerError)
		return
	}
	fmt.Println(string(dump))
	fmt.Fprintf(w, "<html><body>hello</body><html>\n")
}

func main() {
	var httpServer http.Server
	http.HandleFunc("/", handler)
	log.Println("start http listening :18888")
	httpServer.Addr = ":18888"
	log.Println(httpServer.ListenAndServe())
}

```

## 印象に残った箇所 

### 2.3 フォームを利用したリダイレクト

300番台のHTTPステータスコードには送信したい内容がアクセスログに残る危険性があり、それを回避する方法。

### 3.3 コンテントネゴシエーション

クライアントとサーバーでお互いのベストな設定を共有する仕組み。 これによって多言語対応やスマホ対応が容易になる。

### 