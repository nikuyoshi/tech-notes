+++
title = "JJUG CCC 2018 - Autumn"
+++


# アンカンファレンス - 非同期分散、CQRS、イベントソーシング、DDD

* アトミックとなるように厳密にやるよりは、1か0ではなく、中間状態を許容するアーキテクチャとしたほうがスケールする
 * 「結果整合性」という中間状態を許容する考え方もある
 * Amazon S3が有名な例
 * 公式ドキュメント: https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/dev/Introduction.html
   * 結果整合性は、CAP定理でいうところのAPを保証し、最新の状態を取得できなくても確実にデータを返す設計？

# Migration Guide from Java8 to Java11

資料: https://www.slideshare.net/mobile/YujiKubota/migration-guide-from-java-8-to-java-11-jjug
JDK10の互換性リスト: http://git.io/jdk10  
JDK11の互換性リスト: http://git.io/jdk11

## マイグレーションの障壁

ソースコード、バイナリ、動作それぞれの互換性が担保されるようにしているが、互換性が保たれないこともある。
非互換性のポリシー

* APIは最短2バージョンで消える

## 非互換性の追い方

普通はRelease Notesを読めばいいが、載ってないものもあるので、CSRも読んでいるとのこと。

* Issue Tracker
  * JEP
  * Compatibility & Specification Release
  * Release Notes
* Source Repository

## モジュール化を今回説明しないわけ

* クラスパスとモジュールパスの説明をすると時間が足りないため
* Moduleグラフを理解するまではModule化をするには危険。

## Java11化について

* メリット
  * VMのパフォーマンスが上がる
  * G1GCのGCがパラレル化される
* デメリット
  * サポートライセンスを考慮しなければならない
  * バイナリの非互換性

## 対処内容

1. 実行時例外
  * 完全に削除されたオプションの中で、ログGCの移行が特に気をつけないといけない
2. 動作不整合、パフォーマンス
  * `java.home` がアプリケーション側で変更できなくなる

## リフレクション

基本的には使えないように禁止されている。 ただ、オプションを使えば使える。
Java8, Java9以降の両方を対応するライブラリの開発者は、例外を検知した上でリフレクションでインスタンスを
生成するような実装方法になるとのこと。

# Learn JDK11 with JShell

資料: https://qiita.com/nowokay/items/80e8ccd50f6749846dd6

# GCを発生させないJVMとコーディングパターン

## GCの問題

* アプリケーションの実行が止まる
* 割り当てられたCPU時間が減る
  * 健康診断シンドローム
* チューニングが大変
  * 最適解を見つけるのが難しい
  * 環境が変わるとやりなおし
* 見積もりができない
  * GC時間は残存オブジェクトに依存。
* 問題の対処方法としては、以下の選択肢がある
  * あきらめる
  * アプリケーションで頑張る
  * GCで頑張る
  * コンパイラで頑張る


## アプリケーションによる対処

* ArrayList拡張
* Boxing、Unboxing
  * ex. Integerクラス
* String,.intern()
* スレッドプール、コネクションプール
  * プーリングしたほうがGC回数は減るが、一回あたりのGC時間は長くなる

* TLAB（Thread-Local Allocation Buffer）
  * 早いメモリ割り当ては、TLABとBump The Pointerで実装しているとのこと
  * スレッド数が多く、かつオブジェクト青星寮が少ない場合、TLABに向いていない
* `-XX:+PrintAssembly`オプションを追加すると、アセンブリの出力ができる

## コンパイラによる対処

メモリアロケーション量とGC頻度。JVMを変えると、GCの実行され方が変わる。
また、プログラムの書き方も変えると、GCの実行されるタイミングが変わる

## Twitterの声

* GCチューニングする前に、まずはクエリやアプリケーションのパフォーマンスチューニングを行うとよい



