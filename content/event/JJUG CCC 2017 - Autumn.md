+++
title = "JJUG CCC 2017 - Autumn"
+++

## Selenide or Geb? あなたはそのときどちらを使う？

* 資料: 

* テスト用のCSS Selectorを取得するにはChrome Developer Toolを実際に叩く
* Gebを使うには、Groovy, Gradleに関しての知見があるメンバーがいないと導入にコストが高くつく。
* Jenkinsで不安定になりやすい。 Selenium全般の話。 録画機能などを使わないと原因追求が困難。 waitがうまくかからない、など。
* Q&A
  * テストの並列実行をしたいのであればTestSuiteを使う、物理マシンを複数用意するなどした方が良いとのこと。
* 参考: [SelenideよるDSL風E2Eテスト基盤開発の実例](https://speakerdeck.com/shimashima35/example-of-e2e-automation-test-architecture-by-selenide)

## Apache Camel + Hawtio + Spring Bootによるモダンなインテグレーションマイクロサービス

* SOA + ESBといった重量なアーキテクチャを使わずに REST + Message Queueを使ったアーキテクチャを使うのが主流。
* 30台後半のようなベテランエンジニアからすると、マイクロサービスにするとスパゲティ化するのではないかと心配する人もいる
  * 1つのチーム(5, 6名)で1つのマイクロサービスを作るように、組織も小さくしていった方が結果的によい

### Apache Camel

* 軽量なインテグレーションフレームワーク
* 直感的なルーティングDSL
* Enterprise Integration Patterns
* マイクロサービスのサポート(Spring Boot, WildFly Swarm)
* Java DSL
  * fromは1つだけ、toは複数書ける。
* Camel用のIDEA PluginはシンプルにJavaをかけるようなDSLPluginがある。
* JolokiaはSpring Bootにデフォルトで追加されている。
* 280+個のコンポーネントがサポートされているが、それぞれのコンポーネントをどのように利用してCamelに渡すのか、クセがあるとのこと。

### Spring Bootの本当の理解ポイント

資料: https://www.slideshare.net/masatoshitada7/spring-boot-jjug

### アンカファレンス Javaのプロセス監視

* スレッドがハングした場合にどのようにハングしているかを確認するかは、ログの更新日時を取得するしかないのでは、とのこと。
* そもそもスレッド自体を自分で生成するのではなく、フレームワークに任せる方が良い。 スレッドを扱うのは難しすぎるため。
* AppDynamicsのように動的に通信線を引くやり方は、Java AgentとByte Code Intrument(BCI)を使って実装してるのではないかとのこと。

### JDK新しいリリースモデル

* 資料を公開できないが、後日OracleのHPにて見やすい形で公開するとのこと。
* リリースタイミングが、理想とすべき2年間隔となっていないため、リリースモデルの見直しをはかった。
* 多言語はリリース間隔は短いのにJavaはどんどん長くなる一方。。。
* Javaのリリースをするのに、JCPがOKしないとダメ。 Jigsawの時は一度投票が否決された。
* 新しいリリースモデルはJDK 9から開始。 リリースの重複期間がなくなる。

#### 新しいリリースモデル(2017-11-18現在)

* 現在も日々モデルが変わっているため注意。
* OpenJDKを6ヶ月ごとに必ずリリースする。 そのタイミングで完成した機能を入れていく。
* OpenJDKでもバイナリを必ずリリースする。
* OpenJDKもOracle JDKも機能に差分がないようにする。
* OpenJDKのバイナリをGPLv2 + Classpath Exceptionでリリース。 再配布ができるように。
  * JDKを改変した場合に、ソースコードを公開せずにバイナリを展開できるとのこと。
* OpenJDKにJava Flight Recorder(JFR)、Java Mission Control(JMC)、Java Usage Tracker(JUT)が追加される！！
  * Application Class Data Sharing、Z Gabage Collector(マルチテラバイトヒープに対応するガベージコレクション、ポーズを10msにおさえる)、Ahead of Time Compilation(AoTはなくなるかも)
* 長期サポートは2018年0月から開始。
  * Oracle JDKのバイナリで配布
  * 8年の長期サポートの提供
* 更新リリースは3ヶ月ごと(1月、4月、7月、10月)
* バージョン番号が2017.3 → 10, 11, 12...のインクリメンタルな番号に。
* 従来は複数のリリースラインで管理していたが、新しいモデルはメインとなる1つのリリースラインで管理するようになった。
* リリース情報の提供はOpenJDKから提供する。 従来通り。
* JDK 10のリリース情報の提供開始した。
* Deprecatedの運用ルールはそのままで、バージョン2つ分(最短1年)で機能が削除される可能性あり。
  * コルバ(Corba？)関連のクラスが削除されるとのこと。
* 仕様の承認プロセスは従来通りJCP。 だが、ブレる可能性もあり。 
* 公式アップデート終了のスケジュール。 公式アップデートは1年間
  * 8は公式アップデート終了の通知が2017年9月なので、最後は2018年0月。 8から移行するなら11移行を想定している。
  * 9は2018年3月。 9から移行するプランはまだ立っていない。
  * 10は2018年9月。 10から移行するプランはまだ立っていない。
    * 8を利用しているならそのままで良さそう。。。
* 無償の更新期間は光景バージョンリリースまで。
* Java 9以降については、Javaの自動更新は行われなくなる。
* 32bit版のバイナリ提供もなくなる。 移行してとのこと。

### Spring BootとKafkaでCQRS

資料:

* CQRSとは、コマンドクエリ責務分離(Command and Query Responsibilit Segrenetation)のこと。
* DDD
  * 業務の複雑さを改善したいことがきっかけ。 システム最初から作り直したら複雑さが解決できるかというとそうではないと思っている
  * DDDでDBから業務ドメインを引き剥がすことはできたけど、UIは厳しかった。
* Kafkaを簡易的に見るのに、Landoopを使っていた。
* SpringBootを使うなら@KafkaListenerを使うと便利
