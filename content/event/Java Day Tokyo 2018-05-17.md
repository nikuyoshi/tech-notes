# Java Day Tokyo

## Java in a World of Containers

jdepsを用いれば特定のモジュールが使用している依存関係を明らかにできる。
`jlink --compress`を使えば20%以上JDKサイズを減らせるとのこと
Alpine Linuxを使えば小さいサイズのOSとして使えるよ
Class Data Sharingを使えば、コンテナ間のクラスファイルを共有してメモリを節約できる上に、起動時間とフットプリントを削減できる
実験的な機能だが、Ahead-of-Time Compilation(AOT)を使えばJITのように...

JDK10のコンテナにおける設定で以下が参考になるとのこと。
https://mjg123.github.io/2018/01/10/Java-in-containers-jdk10.html

`-m` でメモリの設定をでき、ヒープサイズ、GCのリージョンサイズなどに反映される。

## Running Java applications on Docker: practical tips and valuable insights

### 資料

https://static.rainfocus.com/oracle/oraclecode18/sess/1518180594155001UEZ0/PF/2018-OracleCode-RunningJavaapplicationsonDocker_1524672830935001dCr8.pdf

### サンプルコード

https://github.com/babadopulos/docker-java-issues-demo

### メモリ

Maven内の`java -jar ${JAVA_OPTIONS}`でオプションを設定し、dockerのオプションで`JAVA_OPTIONS`でヒープサイズの最大値を設定すること

デフォルトだと、コンテナは可能な限りメモリを使おうとするため、`-memory`, `-memory-reservation`, `-memory-swap`を設定すること。

### CPU

モンテカルロ法を用いてCPUを大量に使うサンプルで実験した。
コンテナのCPU数を2つに設定したにも関わらず、8つのコアを使おうとしていた。
`--cpu` を設定することを忘れずに。
8コアのCPUを全て使うアプリケーションを2つ同時に動かすと、CPUの取り合いでアプリケーションの実行時間が長くなるが、2コアに絞ったアプリケーションを2つ動かした場合は実行時間はほぼ変わらなかった。取り合いが起こらないため。

### セキュリティ

/dev/random → /dev/

* haveged - simple entropy daemon

### デバッグ

dockerにオプション(JAVA_OPTIONS=ーXdebug etc...)を与えてあげれば、Java Agent経由でリモートデバッグができるとのこと。

### 統合試験

複数同時の実行をする場合は、`docker-compose -p {app-1 or app-2} ...` 
また、Jenkinsを使う場合は、`app-$BUILD_NUMBER`のような設定をすれば自動でビルド番号が入る。

## JDKの新しいリリースモデル

### 検討されていた課題

* 大きな機能の改修にあわせて度々リリースが遅れることがあった。
* スケジュールを優先するか、機能の完成を優先するか？
* クラウド環境に適応しているか？

### 公式アップデート終了スケジュール

8の公式アップデートは2019年1月まで。終了後の更新版入所オプションは商用ライセンスの購入が必要。

### 新しいリリースモデル対応のOracleバイナリ

無償版バイナリはフィーチャーリリース。年4回から年6回リリース。Java SE 8の商用機能が利用可能になる。JFR等。単独で再配布が可能になる。(GPLv2 + ClassPath Exceptionの採用)。ダウンロード先は http://jdk.java.net となる
優勝バイナリは、3年ごとのフィーチャーリリースの特定バージョンに対して設定。Java SE 11からリリース予定。

### OpenJDKに提供される商用機能

* Application Class-Data Sharing (SE 10)
* ZGC
* JFR
* JMC

### ZGC

* スケーラブルかつ低レイテンシのGC。コンカレントGCがベース
* 停止期間が10ミリ秒を超えない
* 数Gバイトからテラバイト上のヒープサイズに対応

### SE 11のバイナリに含まれないもの

* JavaFX(OpenJFXで引き続き利用可能)
* 自動更新機能
* Java Web StartとWebブラウザ用Java Plugin
* 32ビット版バイナリ
* 単独のJRE(JDKからjlinkを利用して生成可能)

### 新しい配布方法への対応

* Web StartやWebブラウザの利用した配布から
  * 主要なアプリケーションストアを利用した配布
  * 企業内アプリケーション管理ソフトウェアを利用した配布(SMS,SCCM etc.)
* システムにインストールされたJREを利用した実行から
  * アプリケーションにバンドルしたJREを利用した実行

### カスタムJREの生成

写真を参考のこと

### 新しいリリースモデル

* 6ヶ月ごとの固定日に機能追加
* CPLv2 + Classpath Exceptionを利用してシンプルかつ再配布可能なバイナリに。

### 従来のリリースモデル

2年に一度の **目標** 。実際には不定期。
OpenJDKは仕様のリファレンス実装。Oracleからの公式バイナリ提供はなし。各ベンダーがビルドしてバイナリをリリース。

### Oracleが配布するバイナリお更新サイクル

12,13,14,15,16に関しては長期サポートがないため注意。

### これからの開発

* 非推奨APIの利用は避ける
* 内部APIの利用は控え、Java Platform Module Systemに移行する
  * 明記されていないAPIは突然削除される可能性あり。
* 不要なモジュールを外す
* 利用しない新機能は気にしない。アップデート・リリースは確認する
* 一つのJarファイルで複数のJava SEのバージョンに対応する
* セキュリティロードマップを確認する
  * https://www.java.com/en/jre-jdk-cryptoroadmap.html

### JDKに付属するツール

画像参考のこと

### 移行に関するドキュメント

画像参考のこと

### Project Portola

* Alpine Linux 上にJDKをポーティング。 musl libc対応。
* jlinkも利用可能。

## Graal: How to use the new JVM JIT compiler in real life

以下の動画がGraalの参考になるとのこと。

https://www.youtube.com/watch?v=G-vlQaPMAxg

GraalはOracle Labsが開発しているOSS。
https://github.com/oracle/graal

スピーカーはJVMに13年近く携わっており、サン・マイクロシステムズ、オラクルでJVMに関するJSRに携わった。
今はTwitterのVMチームにいる。

http://openjdk.java.net/jeps/243

`-XX:+UnlockExperimentalVMOptions -XX:+EnableJVMCI -XX:+UseJVMCICompiler -Djvmci.Compiler=<name of compiler>`

ブートストラップで大量のメソッドをコンパイルする
アプリケーションのメソッドをコンパイルする際、Javaヒープメモリを使う。ただしヒープの分離ができていない。
Graalのメモリは起動時に最も使われる。
mallocだろうが、Javaヒープであろうが、メモリはいつでも使われる。

使うべきGraalVMのオプションは以下の通り

`-XX:+UnlockExperimentalVMOptions -XX:+Enable222222wwwer`

### Demo

OpenJDK 10をインストールするのに、wgetでtarballをダウンロード後、JAVA_HOMEのPATHを通して完了。

```sh
export JAVA_TOOL_OPTIONS="-XX:+UseParallelGC -Xmx512m -Xms512m"
```

`java -version`で適用されたか確認すること

### Performance tuning with poor tools and cheap drink

資料
https://www.jfokus.se/jfokus17/preso/Using-jPDM--a-performance-diagnostic-model.pdf

上記資料の34ページの問題分析のフローチャートが参考になる。
`vmstat`の`us`:ユーザー領域、`sy`:システム領域のCPUを見るなどして問題解析をしていく。

* JPDM(java performance diagnostic model)とは？

#### Demo

VisualVMを使ってスレッドダンプの解析、およびMacのアクティビティモニタで CPUの使用率を確認していた。
文字列結合に`+`を使っていた箇所を`new CompositeKey(hoge, fuga)`に変換 