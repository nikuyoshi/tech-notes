# JJUG CCC 2018 Spring

## Swagger(OpenAPI Specification)入門

* SwaggerとはRESTベースのAPIのためのドキュメンテーションフレームワーク。
* 2015年にOpen API Initiativeに寄贈された。
* Programmable Web
  * https://www.programmableweb.com/
* 事例: Fidor BankのAPI
  * https://api-docs.fidor.de/v1/introduction/welcome-text
* Generation Gapパターンの適用
  * 自動生成されたクラスを継承してカスタマイズする。
* Swagger Hub
  * https://swaggerhub.com/

## LINE LIVE のチャットが 30,000+/min のコメント投稿を捌くようになるまで

### 全体構成

* WebSocket
  * Aerver Clientの通信
  * 単一のコネクション
  * 双方向のメッセージング
  * 低いレイテンシ
* akka actor model
  * Server内での高速な並列処理
  * 高い障害耐性
    * メッセージが大量に流れるため。
  * 軽量スレッドによる高速な並列処理
* Redis Cluster
  * Pub/Sub Server間のメッセージ同期、高速なKVS
  * コメントや各種データのキャッシュ
  * Lua Scriptingを使ったatomicな処理

### チーム構成

* もともとPerlを書いていたメンバーが初めてJavaを書く案件となった。
* 2015年から始めた案件。
* 当時Java 8が流行ってきていたため、新しい流儀に慣れるのが大変だった

### Perl vs Java

* Perl(マルチプロセス)
  * Parallel::Prefork
  * Parallel::ForkManager
* Java(マルチスレッド)
  * java.util.concurrent package
  * ParallelStream

### 課題

* 共有されるメモリ空間
  * スレッドセーフにするのは大変
* スレッドセーフ
  * コンテキストスイッチがどの程度負荷がかかるのか

### akka

* akka Actor Model採用の着目点
  * 割り当てられた単一の軽量スレッド上でのみ実行されるため、スレッドセーフであることは大変助かったとのこと。
* Actor間の疎通
* Supervisorによる監視
  * One-for-One strategy
  * All-for-One strategy
* 通信に関して、非同期通信を心がけた。通信が残りっぱなしかどうかはWatchdogを使って、一定時間以上残っていたら通信を切るようにした、とのこと。

## いかにデータが壊れない管理画面を作るか

### SmartNews Adsについて

コンテンツ広告を拡大していく広告プラットフォーム

ex1. スマートニュースアプリへの広告配信
ex2. ターゲティング。ユーザー属性によって広告配信先コントロール

### アーキテクチャ

SmartNews Adsでは、汚れ役を立てて、それ以外を綺麗に保つという設計にしている。
* 汚れ役
  * サブコンポーネント間の接続点の仲介
    * 管理画面は多くのコンポーネントに接続する必要がある
  * データを利用しやすい形で正確に保つ
    * データの利用側は、ある機能が機能するための最低限のvalidationだけを意識すればよい
    * validationをきちんとしていれば、他のコンポーネントは例外に関して意識しなくてよくなる。
* コンポーネント間の仲介
  * SmartNews Adsでは、基本、直接の依存コンポーネントを極力減らすという判断をしている。
* Meshか、Lineか
  * Line型を選択。両者の制約を吸収することによって、互いの進化のスピードを落とさない。
  * Mesh型も、開発スピードはあがるが、依存度があがってあとで辛い。

### データについて

* SmartNews Adsにおいて、広告配信に最適なデータ構造を意識した。
* 管理画面の開発は、その設計をフォローする形で始まった。
* 解くべき問題が、Ad ServerとAd Frontendで違ったため、データ構造をそれぞれ買えている。
* データベースにドキュメント形式(JSON)で持つようにすることで、動的性と拡張性を柔軟に。
  * スタートアップによってスピードを最優先するために、ドキュメントフォーマットを選んだ。
  * Document形式を定義するのはDMP。

### データの強制力について

フロントエンド
↓
コントローラ
↓
サービス
↓
リポジトリ
↓
データストア

の順に、データの元に近づけば近づくほどデータに対するルールの強制力は強くなっていく。

リポジトリでデータの制約を守る最終防衛ラインをはって、バリデーションをしている、とのこと。

## アンカンファレンス(Javaの話)

### 非同期の話

* .NET でいう `async` `await` をJavaでやりたい
  * → Javaではない。 書くのは大変。
* ReactiveなものをJavaで書こうとするとだるい。 RxJava、Akkaとか。みなさんどうしてますか？
* GoはJavaよりコンピュータに直接命令する感じ。
* 非同期でやる手法
  * 新しいスレッドを起こして通信させる
  * メッセージキューを使う手法
* OSスレッド
  * グリーンスレッド
* Spring Boot 2.0から非同期の書き方が大きく変わる。
* 簡単に

### メモリの話

* プリミティブはスレッドスタックに乗る。
* クラスのデータはヒープ(PermGen)に乗る。
* インスタンス生成すると、ヒープに乗る。
* 値渡しと参照私は「Java本格入門」がオススメ。「Java Performance」もオススメ。
* スタック、ヒープをきちんと学びたいならCを学べば分かるはず。
* Optimizing Javaもオススメ。

## アンカンファレンス(情報収集について)

### 情報収集について

connpassのイベントを集約してメールを送ってくれるサービスがあるらしい。

### 学校教育について

大学ではプログラミングの理論、アルゴリズムを学ぶにしても
情報工学を学ぶにあたって、前提となる条件が違う。

## Java のデータ圧縮ライブラリを極める

* データ圧縮アルゴリズム
  * Deflate
    * 2010年台まではデファクト
    * メモリフットプリントが圧縮時でも数百KBと小さくて済む
    * 速度性能が求められる場合はLZO。ただしGPLv2
  * Zopfli(Deflate)、Guetzli(JPEG)
  * Snappy
    * Google製
    * LZ77をベースとしたアルゴリズム
    * 圧縮、復元の処理速度が早い
  * LZ4
    * 復元処理の速度を重視している
    * 利用実績がとても豊富。Linux, FreeBSD...
  * Zstandard
    * Deflateと同等化、それ以上の圧縮率および処理速度を達成する
  * Brotli
    * HTTP圧縮におけるエンコーディングの一つ。
* Javaにおける圧縮
  * snappy-java
    * 多様なOS / アーキテクチャをサポート
  * lz4-java
  * zastd-java
  * jbrotli
* Javaではどの圧縮アルゴリズムを選択すべきか？
  * 処理速度を重視: LZ4, Snappy
  * 圧縮率を重視: Zstandard (,Brotli)
  * 対応しているOS/アーキテクチャの多様さ: Deflate(JDK Built-in)、LZ4(pure Java)
* Dockerコンテナ内での利用は、Alpine LinuxとJNIとの互換性には注意すること
* 復元率、圧縮率に関しては資料の表を参照のこと。

### まとめ

圧縮率と処理速度のバランスを重視するなら、Zstandard
処理速度重視であればLZ4

## ビジネスとオープンソース - 戦略と手法 -

98.5%は企業に勤めた人が書いていて、残りは他の人が余暇でやっている(OSSの○○の話)
Stackoverflow、GitHub、Wikipedia、mozilla、Slack、Blizzardの裏側でElasticsearchを使っているとのこと。

### OSSで稼いでいる企業

* CANONICAL
  * Ubuntu
* Red Hat
  * RHELで稼いでる
  * 772M$

使いやすいと問い合わせが来ないため儲けられないが、使いにくくすることはできない。
安くコンサルを行っている企業が出てくると、本家のコンサルが売れなくなってしまう。

### Open Coreの例

* MySQL
* MAPR


クラウドプロバイダーの問題
ベンダーロックインを避けられてしまう問題

### 自社でクラウドサービスを提供しているサービス

* WordPress
* Sentry

### 自社のサービスをクラウドで提供させないようにした事例

* mongoDB
  * AGPL
* CosmosDB

### Partner Ship

* FireFox
  * デフォルトで提供する検索エンジンにする(Google等)

### 寄付でも儲けている企業

* Wikipedia
* moodle

### グッズ

* OpenBSD

### クラウドファンディング

* Cataslysm
* Dark Days Ahead

### ビジネス

OSS版、エンタープライズ版両方用意すると、エンタープライズ版ばかりメンテナンスしていってしまうことが問題になる。がめつい。
dockerはどのような形で儲けたいのか分からない。。。

### Open Source vs Open Code

* Open Code
  * CockroachDB
  * Elasticsearchも同様にしている。
  * コードは公開するが、使うときはお金ください、という形式。
  * OSS版とエンタープライズ版とを一つのリポジトリで管理できるようになった。


PostgreSQLは支援されなくてもうまくいっている。

