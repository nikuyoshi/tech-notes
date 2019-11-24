+++
title = "JJUG CCC 2019 - Fall"
+++

# JJUG CCC 2019 Fall

## Head toward Java 13 and Java 14

資料: https://www.slideshare.net/YujiKubota/head-toward-java-13-and-java-14-jjug

### Java 13

5つの機能追加。1378個のバグ修正
* Dynamic CDS Archives
  * Class Data Sharing。共通的なクラスや文字列などを複数プロセスで共有する機能。起動時間を短縮できる。後出しできないので異常系を含めてロードする必要あり
* ZGC: Uncommmit Unused Memory
  * ZGCが未使用のメモリをアンコミットしてOSに返すようになった。Xmsは下回らないようになっているので、XmxとXmsが等しければ自動的に機能が無効になる。
* Reimplement the Legacy Socket API
  * Socket API(java.netSocketやjava.net.ServerSocket) の内部実装が変わった
* Switch Expressions (Preview)
  * Switchの戻り値を示すステートメントが break から yield に変わった。
* Text Blocks (Preview)
  * ヒアドキュメント。文字列を書いた通りに読み込むことができる。提供されるクラスは `@Deprecated` が付与されているため、今後変更されたり消される可能性あり。
* Unicode 12.1サポート。
* Java 5時代からていあんされていたBufferのAPIが追加された。
* -Xmsは正確には亜初期サイズであり最小サイズではない
  
### Java 14

8 + 5個の新機能

* NUMA - Aware Memory Allocation for G1
  * NUMA nodesを意識してheap regionの配置を行う
* Pattern Matchingg for instanceof
  * instanceof で確認した後にキャストしなくても良くなる！！
* JFR Event Streaming
  * ディスクに書き込まれたバイナリデータをストリームで取り込めるようになる
* Helpful NullPointerExceptions
  * NPEを出した場合にどこで起きたのか、分かるようになる
* Remove the CMS
  * 非推奨になっていたCMS GCがついにソースコードから削除。
* ZGC on macOSs
  * macOSsにも移植された。Windowsはこれから。
* Remove the Pack200 Tools and API
* Packaging Tool (Incubator)
  * JavaFX javapackagerをベースにパッケージングツールを提供
* Records
  * 構図かされたtuplesのようなもの。
* Text Blocks
  * 改行 `\` と空白 `\s` を柔軟に制御できるように2つのエスケープシーケンスを追加した
* Deprecate the ParallelScanvenge + SerialOld GC Combination
  * Young領域はParallelでOld領域はSerialでGCを実行するという組み合わせが非推奨された

### OpenJDK Forks

独自のJDKがどうなっているのか確認してみた

#### OpenJDK

厳密にはメンテナンス期間は確定していない。OpenJDKコミュニティのメーリングリストでメンテナンス終了の通知が行うあれ、メンテナンスを引き継ぐコミュニティなどが現れないとそのまま終了とする。 JDK 9、JDK 10、JDK 12は引き継ぎ先が現れず終了。

#### Eclipse OpenJ9

JDK部分ではなくJVMのオープン実装。 JDK部分にOpenJDKを利用したバイナリがAdoptOpenJDKコミュニティで配布されている。そのため、JDK部分のメンテナンスは実質AdoptOpenJDK。

#### AdoptOpenJDK

Java11は `jdk-updates/jdk11u` をベースにしていて、メンテナンスはOpenJDKに準じる

#### Amazon Corretto

Java 11のリポジトリでupstreamでタグうちされたタイミングでmergeしているようだが、squashされてて一見では確認不可能。 mergeもPRでmergeパターンと直接Pushパターンがある。 upstream先が分からん。

#### RedHat OpenJDK

Linux Distribution提供のopenjdkパッケージは提供元のパッケージソース。 RPMパッケージであればRPMS(SPEC)を確認。

#### Ubuntu

メンテナンスきかんはOpenJDKコミュニティに準じる

## 入門例外

発表資料: https://github.com/mike-neck/practical-exception

ビールの販売を例に、例外がなんなのか、事前条件、事後条件とは何かを伝えた上で何故例外が大事なのかを説明。その後ビール販売を例に具体的な実装例を説明していた。例外伝播、デフォルトコンストラクタを使わない等、例外実装の基本を復習するのによかった。

## Reliablitity Engineering Behind the Most Trusted Kafka Platform

LINEのKafka運用について。
Kafkaをどのように
Kafkaを使うにあたって、Reabilityや汎用的な話について話す。
各システム間のイベントプロパゲーションのハブとして、非同期のバックグラウンド処理として分散キューイングとして使われている。
360Billionのメッセージフローが1日に転送しており、1日550TB、サービス間は60以上。単一のKafkaクラスターであれば世界最大。
Service Level Objective(SLO)について。99.999%のCluster Availability、とあるAPIの99th Percentileは40ms。
SLOの可視化は、オペレーションの自動化について注意している。
SLOの可視化については、APIのレスポンスタイム、エラーレイトを測っているだけでなく、クライアント側のリトライ、フェイルオーバーにかかった時間についても注視しているとのこと。中の処理を具体的な数字を取得している。
Proberというコンポーネントを作って、クライアントから見たクラスターの性能を計測している。SLIのダッシュボードも提供しており、障害の兆候もわかるように。
Writer、Reader、

### トラブルシューティング

KafkaのGCの問題が起きた場合、暫定対応と恒久対応の中でも恒久対応を優先することを是としている。
JVMのsafepoint syncの時間が伸びていたこと、
Write System Callが2秒越えしていた。safepointの中から呼ばれていることもわかった。Write System Callはブロックする。
kprobeを利用することで、linux Kernel APIでDelayを加えて再現ができた。
EXT4のジャーナリングがつまると、Writeをしているアプリケーションがブロックされることは分かった。

## JavaオンプレシステムをAKS + Quarkusに移行した話

資料: https://speakerdeck.com/takaichi00/jjug-ccc-2019-fall-javaonpuresisutemuwoaks-plus-quarkusniyi-xing-sitahua

移行の泥臭い話を聞きたかったけどQuarkus中心だった。

## アンカンファレンス - JVMの何か

OOMで止まる時に、クラッシュするオプションを使った方が、コアダンプが取れるのでいざという時に役立つのでオススメ

## Twitterとかで見た情報

https://www.slideshare.net/tyoshio2002/jjug-ccc-2019-fall-azure-spring-cloud

Microsoft社とPivotal社が提携した

https://remkop.github.io/presentations/20191123/index.html
PECOCLIを使えば、バイナリ生成できる。CLIの補完用のスクリプト生成(Bash, Zsh)、出力の文字色対応もJavaのアノテーションで実装可能などJavaエンジニアがコマンド実装するには良さそう。 バイナリということで起動も一瞬。

https://speakerdeck.com/rshindo/jjug-ccc-2019-fall
OSSのソースコードの読み方。 taichiさんのやつと読み比べたい。

## Javaの起動速度といかに戦うか

### 起動速度が注目されるようになった背景

マイクロサービスとして多数のサーバーを不可にあわせて伸縮することが求められるようになった。

### 起動を早くするアプローチ

* クラスファイルの解析をあらかじめ行う
  * 解析したクラスファイルメタデータを使い回す。 実装: OpenJDK CDS(Class Data Sharing)。
  * Java 10からApp CDSが使えるようになった。
* JITのためのプロファイルを使い回す
  * 実行時に収集したプロファイルデータを次回の実行や別のjvmで使い回す
* JIT結果を使い回す
  * 実装: Openj9、Azul Zing
* 同種サーバーでJITを共有
  * OpenJ9 (JIT as a Service)
* あらかじめコンパイルする
  * 実装: GraalVM native image、Java 9 AOT
  
JITとAOTの比較。AOTの方が起動時間が早いがスループットがJITに比べて劣っている。
それを改善にするために、GraalVM EEではJITで収集したプロファイルデータをネイティブイメージで使えるようなるとのこと。

### ベンチマーク

Micronautを利用。

#### OpenJDK
  
Java8 → Java13の差
AOT、CDSとではあまり差がでなかった。Java 8をJava 13に変えるだけで、それだけでも大分速いとのこと。
Java 12からでDefault CDSで最初からCDSが効いている。

### HotSPot以外のJDK

起動時間の比較は資料参照のこと
Azul Zingは起動を速くする用途ではない。

### GraalVM native image

起動時間は圧倒的に速い。が、に
スループットが悪い。
メモリ使用量はGraalVM JITは大量に食うが、GraalVM AOTは削減されている。

### Java 14移行で入るかもしれない機能

* static finalフィールドの遅延読み込み
  * `private final static Logger LOGGER` とかが必要な時に遅延読み込みされる
* GraalVM JITコンパイラのプレコンパイル
  * OpenJDKに含まれているGraal JITはJavaで書かれているので、それ自身のJITが必要。
  
### まとめ

OpenJDK自体の起動速度もApp CDSが追加されたため、Java 12以降であれば高速に動く。
GraalVM使わなくてもそれなりに対応できる。

## 多言語対応の仮想マシンGraalVMが照らす未来

GraalVMに初めて触れる人に概要を伝えることが目的。
近年のJava界隈で人気が出てきている。
あらゆる言語をJVM上で実行できるもの。ユニバーサルVM。
あらゆる言語の実行環境となれる能力がある。
JVMでできることはGraalVMでもできる。
Truffle 言語実装用のライブラリ。JavaScript、Ruby等はこれを使ってTruffle Ruby等として実装されている。JavaScript以外はExperimental。
Community版を使えば無料で使える。EEはCEより120-130%近く性能が高い。 Oracle Labsが開発しているため、研究成果として製品が上がっているような背景がある。
EEはOracle Cloudを使えば無償で使える。
パフォーマンスを大幅に低下させることなく言語間で相互呼び出しができることがGraalVMの主の目的。
→ コンテナは？

Graal VisualVMもあるため、呼び出し等も確認できる
Chrome Dev Toolでのデバッグも可能

JITコンパイラも自分で作れるが、最終的にCPUの呼び出しリファレンスも必要になってくる。

ゴールドマンサックスでオレオレ言語を作っていたが、Truffleベースに移行したとのこと。
自分で作ったオレオレ言語がGraalVMで動く！！

ネイティブイメージ生成の話。Oracle DatabaseにGraalVMを組み込んで複数言語に対応できるようにするプロジェクト内で、起動時間、消費リソースを減らす目的で、社内事情でネイティブイメージ化する必要があった。その出来が良かったため公開されたとのこと。
ネイティブイメージ生成には時間かかるため、そこは注意。
Java om iOS！！ iOS上ではJVMは禁止されているが、ネイティブイメージならOK。
どんなアプリケーションでもネイティブイメージでも良いかというとそうではない。
ネイティブイメージが適しているのは起動してすぐに停止するもの、マイクロサービスのようなもの。Micronaut、Springのようなフレームワークも対応しているものもある。

Substrate VM
リフレクションもネイティブイメージ生成時に自動で判別できるものもあるが、できないものについては設定ファイル書く必要あり。
GraalVM 19.3からJava 11も対応。年間最後のリリースはLTS。

バイトコード + プロファイル → マシンコード
JITもAOTも技術的には似ている。

## JVMs in Containers: Best Practices

`#ccc_I7`

Serverless Java function - OpenJDK 13
Alpine Linuxディストリビューション用のJDKを用意するプロジェクトとして、Portolaというものがある。

https://openjdk.java.net/projects/portola/

コンテナの内部情報可視化としてdiveというツールを使っていた
https://github.com/wagoodman/dive