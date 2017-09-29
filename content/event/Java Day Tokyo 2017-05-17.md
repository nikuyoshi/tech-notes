+++
title = "Java Day Tokyo 2017"
+++

## 基調講演

### 杉原博茂

* Oracle Japan VISION 2020 日本を幸せにするクラウドカンパニーへ
* Javaが日本を幸せにする
* 日本には多大な課題がある。
  + 働き方改革、人手不足...
  + ITSにの人手不足が特に目立っている
  + 2030年には約60万人の人手不足に
  + Oracleが提唱するのは百人力。 生産性向上。
  + 日本のIaaSと関連するITSに製品&サービスの実態
    - オンプレミスで使用している経費が高すぎる。 IaaSだと2100億円で済むのにオンプレミスだと12兆円かけている。
* TIOBE プログラミングコミュニティインデックスで1位
* Java 22年目

### Bernard Traversat

* ｢Java is dead.｣は常に言われ続けてきた。 Oracleが買収してから言われなくなった
* OpenJDKのアクティブなコミッターは136%増えた。
* No.1の開発環境としてJavaは存在する。 今はクラウド上でも。
* 世界中で使用されているJava。97%のエンタープライズデスクトップで使用されてきている。
* Javaの哲学
* クラウド上でのJava SE
* DockerとJavaとの親和性について
* Java 9 Features
  + Project Jigsaw
  + 122の新しい機能。 19の機能はインテグレート、クローズした。
    - JEP 261 Module System
    - JEP 200 The Moduler JDK
    - JEP 222 JShell
    - JEP 295 AOT
    - JEP 282 jlink
    - JEP 260 Encapsulate Internal APIs

* Beyond Java 9
  + Project Valhalla
    - Value Types
    - Specialized Generics
    - Var Handles
  + Project Panama
    - Foreign Function interface
    - Date Layout Control
    - Arrays 2.0

#### Masahiro Yoshioka - Staff Manager, IT Solution Div. Mazda Motor Corporation

* ロードスターの製造工場の中でJavaを使用している。
* Assembly Line Controlという仕組みを使用している。
* 1つのラインで複数の車種を製造している

#### MazdaとJava

* 従来型
  - 機能要件･非機能要件を満たすのは必須。TCO、生産性の工場。
  - すべての開発者は共通のアーキテクチャ、共通のフレームワークを使用している。
  - 基幹系の業務アプリケーションは長く使われる。 言語が長生きするのは重要なこと。また、下位互換性も重要
  - 数百GBのデータを使用している。

* 問題
  - 要求をすべて取り込んでいくとシステムが複雑になる。 Jigsawに期待している。
  - GCの問題がある。

#### Shinya Yoshida - OpenJDK Committer

JShellの紹介
REPLでインタフラクティブな操作が可能となる。

#### 自転車競技における定量化手法による強化事例紹介

全日本選手権で2度優勝している。

スポーツの現場でJavaを活用している事例

* 定量化としてのパワーメーター
* 目標とするレースが要求する能力の可視化
* 自動車データ分析支援システムのソフトウェア概要
* 最適なギア比を把握するたえに可視化をしているとのこと。

### Java Enterprise Edition Update - WIll Lyons

* Java EE Evolution
  + Enterprise Java
  + Robustness
  + Web Services
  + Ease of Development

* Java EE - Available On Premise and in the Cloud
* Java EE APIs - Backbone of Leading Open Source Projects
* Java EE 8 Improvements for Cloud and Microservices

#### Java Community Process

開発者と各会社に議論する場を提供している
今年で15周年

#### JJUG CCC

今週末に実施予定

### 感想

* 見る限り2016年の基調講演と資料が被っているものがあった
* クラウド上でのJava利用について強く言及していた。
* セキュリティに関して問題ないと言及がされていた。 完璧なセキュリティとか言っちゃって大丈夫だろうか。。。
* Jigsawがコミュニティから否決された件が一切言及なし。
* 基調講演のデモがJavaならではのネタが一切なかった。 それPythonとかでもできるじゃん、なんでJavaじゃないとダメなのかが分からん

## Java 9 and beyond

### Java 9

* セキュリティのプライオリティを最優先にして対応している
  + クラウドにセキュアにデリバリーできるようにしている。

#### Java 9 Features

* Jigsaw
  + セキュリティ
    - どのAPIが、どのサービスを外部に提供するのかを明示化する
    - RMIを外部から攻撃されないように隠蔽する
  + jlink

* Ahead of Time(AOT) Java Compiler
  + static コンパイラとダイナミックコンパイラを合わせたもの

* JShell
  + REPL
  + 今まで使用できたAPIを使える

* G1 GCがデフォルトに

### Java SE Advanced

ミッションクリティカルなサービス向け

#### Flight Recoder Performance

* オーバーヘッドが極めて低くなった。 商用環境で常に起動していても1%以下となる。
* Recording Template
* Direct Insight in the code
  + メモリリークが起きた時にどのコードが原因なのかを追求できる
* Advanced Management Console - The way it works

#### Java Object Data - Project Valhalla

* codes like a class, works like an int!

#### Improved Java/Native Interoperability - Project Panama

### Beyond 9

## Modular Development with JDK 9

### Programming In the Large

複数のパッケージをまたがってAPIを公開するにはpublic修飾子をつけて公開するしかなかった。その問題を解決するのがJigsaw。

* public to everyone
* public but ony to specific Modules
* public only within a module
* 公開されていないPackageにアクセスするとコンパイル時にエラーが起きるため、実行時例外で初めて見るということはない。
* JDKの使用していないパッケージを省いてデプロイすることができる。 デプロイするモジュールサイズの削減が可能。
* 必要なモジュールが足りない場合、そのモジュールを使用したタイミングで発覚するのではなく起動時に必ず分かるようになっていること
* 循環依存、参照がないようにする。 循環する時は開発のバグであるとのこと。

### Migrating To Modules

* それぞれのJarファイルはモジュールとして良い候補になりえる
* それぞれのJarファイルは自分のペースでモジュラーになりえる

### The Modular JDK

* JDK9にあがると、リフレクションを使用している箇所でデグレが相当出そうとのこと。
* rt.jar, toolsjarが無くなる
* -Xbootclasspath/pが使えなくなる
* シマンティクスバージョニングに変わる

## Introduction to JShell: Official REPL Tool for Java Platform

### Introduction to JShell

* public, final等の修飾子は無視される。
* synchronizedは無視されない。

* JShellのコア実装APIを叩けるのはOracle JDKとOpenJDKのみ。
* Debugコマンドを使用すると、JShell内部の挙動を確認できる。

### Integration of JShell

JavaFXをJShellから呼ぶには、JavaFXのスレッドを呼ばないといけない。
外部から呼び出す際は、Maven Pluginを使用すれば楽できる。

### Q&A

* JShellはスクリプトファイルにできるか → できる。
* JShell内でThreadを生成して実行するとどうなるか → 普通に生成される。 別VMで動いているため、クラッシュしてもJShell上には影響ない
* 教育ツール、開発時の便利ツール以外の用途はあるか？ → 試して教えて欲しい。CLIとして使用している人もいるとのこと
* JShellの仕組みで、RemoteExecutionControlで別のJVMを呼び出す理由について → 他のユーザーがSystem.exitを実施した時に影響を受けるため。
* thisは使えるか → トップレベルで使うことはできない
* いつも使うようなライブラリ(commonsなど)を常にパスに通しておくような機能があるか → ない。 頑張ればできる。
* セミコロンが省略できない場面は？ → 入力の末尾になっていない場合。 if分、メソッドのブロックの中など。実際に触って試して欲しい
* 製品版での利用は想定されていないのか → 想定していない。 パフォーマンスがでない可能性がある。 JShellのJVMとコード実行のJVMの両方が立ち上がるため。
* GroobyConsoleとの差異は？ → 使用したことがないためよく分からない。 Javaの経験が浅い人は使えるはず。
* 一度importしたクラスをあとでimportから外せるか → dropコマンドを使用すればできるはず
* ステップ実行はできるか → できない

## CDI 2.0

* 仕事の電話応対をしていて途中退出を繰り返したためメモなし

## 感想等

* 今回のイベントではほとんど言及がなかったが、JigsawはJava 9では恐らく使えない。 JCPでの否決がされたため。
  + 先週Jigsawが否決されたことが何もなかったかのようにセッションで話していたのに驚いた。
