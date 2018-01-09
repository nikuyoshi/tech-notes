---
title: "Ansible Night in Tokyo 2017.12"
date: 2017-12-21T19:09:17+09:00
draft: true
---

### 19:10 - 19:50 「2017の〆に抑えるAWX&AnsibleTowerの活用!!」 HPE 北山さん

資料が公開されてない模様(2018-01-09時点)

* Ansible Towerの紹介
  * 覚えるべき概念
    * 組織
    * インベントリ
    * チーム
    * プロジェクト
    * ジョブ
* Ansibleの各モジュールのサポート
  * CoreモジュールはAnsibleのコアチームが管理して安全な状態で使える。
  * Certifiedはベンダー用のモジュール。

#### Ansible Towerの使い所

* Ansible Towerに企業内のAnsibleを集約
  * そもそも役割担当者ごとに入るホストが違って、NWも違うから個別にあれば良くないか
  * となりの組織のPlaybookとか実行しちゃったときには何言われるか分からない
* ユーザー権限管理
  * Playbookの実行権限、結局はホストへのアクセス権限だから今までの管理で良いのでは？
* 履歴管理
  * ansible.log取ってるけど何か？
* オペレータ用の画面

#### Ansible Towerの使い方
    
* 運用自動化とは、運用業務をコードレベルまで標準化して実装まで行うこと。
* 標準化できるならやればいいけど、標準化が正義ではない。 工数が大きいし、実装レベルも求められる。
* 運用自動化に期待しすぎると、駆使しすぎる自動化環境を作成してしまい、最終的には誰も変更できずにオートメーション恐怖症を生み出す。
  * 汎用性の高い夢の自動化を作るのではなく、出来る限り疎結合となるような汎用性の高いPlaybookを作ることが大切。
* Playbookでいうならば、
  * Codeの疎結合化
  * Codeのテスト徹底的に行う。
* Workflow Job Templateのススメ
  * ワークフローを利用することで、疎結合かつテスト自動化を柔軟に行える。
  * 頑張らない自動化
* まずはSimpleなワークフロー管理から始める。

#### Ansible Towerつきハードウェア

* HPE Synergy with OneView
  * Baremetal as a Service
  * Ansibleからハードウェアを操作する
  * スケールアップも容易？
  * [GitHub: oneview-ansible](https://github.com/HewlettPackard/oneview-ansible)

#### まとめ

* Ansible Towerを利用することで、運用自動化を見直す。 Codeの疎結合化、Codeのテスト徹底。
* 完全標準化することの意味はなく、Engineによって苦労していることを頑張らずに自動化を行う一つの解がAnsible Tower。
* Ansibleで取り扱えるものは今後も増える。

### 19:50 - 20:30 「OpenStackをAnsibleで操る！」クラウド運用における活用事例紹介 富士通 岩松さん、下國さん、本田さん

[資料](https://speakerdeck.com/r0ckpine/openstackwoansibledecao-ru-ansible-night-in-tokyo-2017-dot-12)

* FUJITSU Cloud Service K5の開発チームメンバー
  * http://jp.fujitsu.com/solutions/cloud/k5/

#### K5とリリース業務

* 世界9リージョンで提供中のIaaS。 OpenStackがベース。
* 月刊数百件のリリース。
* リリース業務とは、新機能提供、機能修正のためにサービス全体を停止せずにソフトウェアを更新する。
  * LB切り離して片系運転、片方をアップデート、アップデート終わったらLB切り戻しなど
  * OpenStack CLIを駆使して、状態正常性を確認しながら手順書通りに行う高度な作業
* Ansibleを導入する以前は指差し確認。 作業履歴はターミナルログ。
* 効果としては、数百台への緊急修正適用時間を大幅短縮、作業ミスゼロ。
  * Playbook開発とテストは1.5時間。 導入前から一人あたり60時間の工数削減。
  
#### 適用半数を厳密に守る

* 更新するパッケージ群とそのバージョンは厳密に指定する。
  * 指定パッケージのパッケージがインストールされる。
* 意図しないパッケージの混入を把握、対応する

```yaml
rpm_packages:
  - name: curl
    version: 7.29.0-...
  - name: dhcp...
```

* 適用前後のrpmの比較を確認する
* 席用前後の差分リストからarchを削除
* 意図したパッケージとの比較
* 意図しないパッケージがインストールされていれば例外を出す 

#### 手順を間違えない

* 複雑なデータをパースする際は、すべてをJSONにして、`json_query`フィルタで扱う。
  * `grep`, `awk`, `shell`でパースをするのはNG！！
* json_query`フィルタとは、複雑なJSONデータをqueryするフィルタ。
  * JSONのメンバやスライスを抽出。
  * 構造体のリストから、条件に合致する項目を抽出して、リストとして出力。
  * `jmespath`のクエリを使う
    * http://jmespath.org/
    * 内包表記を`json_query`なら似たような書き方ができる。
* すべてのOpenStackの操作をJSONにして管理する。 
  * `openstack server list -f json`
* Playbookの中にshellスクリプトを持ってきただけでは辛い。
  * `prettytable`をJSON形式に出力するフィルタモジュールをOSSで公開予定。
* `map`、`reduce`のような加工をしたい時は、`f_x() for x in source_list]`をAnsibleのタスクで実現。


#### 適用対象を間違えない、履歴を残す

* AnsibleだけではPlaybook･適用対象を管理しきれないため、GHE, Jenkins, Foremanを使っている。
* Jenkinsfileでジョブを定義。 
  * テキストなのでGitで管理できる。
  * ブランチごとにジョブを作成。 multibranch pipeline というPluginを使っている。 超便利らしい。
    * https://wiki.jenkins.io/display/JENKINS/Pipeline+Multibranch+Plugin
* Excelによるサーバー管理をしていたが、 `yaml`に変えた。 リージョン単位にインベントリを管理しても管理が破綻したため、Dynamic Inventoryを管理するようにした。
  * コミュニティ版多数あるため、そこから選べば良い。 FujitsuはFOREMANを選択した。
  * Foremanは、OSSのサーバープロビジョニングツール。 Dynamic Inventory対応。
  * `ansible-playbook -i foreman.py`
  * Jenkinsで履歴管理を行い、作業者、結果等Jenkinsから全て参照可能。 

#### まとめ

* 複雑なOpenStackの運用にも、Ansibleは使える。
  * 厳密な処理確認をPlaybook化
  * 出力データをJSON化
  * ForemanによるDynamic Inventory化
  * Jenkinsによる履歴管理
* 今後の課題
  * Ansibleコミュニティへの貢献
  * 作った人がいなくても持続できる運用

### 20:40 - 21:00 LT (5 分 x 4〜5人) ＊前倒しして開始します。
#### ▷ 「AnsibleとPackerでゴールデンイメージを作成する」 @curry9999

資料が公開されてない模様(2018-01-09時点)

* データベースアーキテクト。
* Ansibleのモジュールの歴史をブログに載せている。
  * https://awsbloglink.wordpress.com/2017/10/10/ansible-%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB%E3%81%AE%E6%AD%B4%E5%8F%B2/
* ゴールデンイメージとは、仮想マシンのイメージのこと。 イメージにOSやアプリケーションの設定を含める
* Packer
  * HashiCorp製のOSS。
  * BuildersとProvisioners

#### ▷ 「ansibleで1年間運用して感じたこと」 @Oh434b0S7nigh27

電話応対をしていたためメモ取り損ねた

#### ▷ 「Ansibleに貢献してみよう」（仮） @shigemk2

[資料](https://www.slideshare.net/shigemk2/ansible-84772376)

* Ansibleのドキュメントに関するtypo、リンク切れ、リンク先の変更を変更した。
* Ansibleのドキュメントの特徴
  * GitHubで管理
  * ドキュメント生成ツールはSphinx。
  * ドキュメントの内容が細かい。 CoCなど
  * OpenなままのIssueやPRが超多い。 4桁。typo系のPRは割とすぐにマージされる。
* 修正のサイクル
  * 修正のサイクルは、PyCharmでtypoを探して直す。
  * buildして、ブラウザで見る。 バージョンなどはN/Aとしている。
* ドキュメントを更新し続けるのは難しい。 by レガシーソフトウェア改善ガイド

#### ▷ RancherがみつめるAWX @tsukaman

[資料](https://www.slideshare.net/tsukaman/rancherawx)

* 以下の記事を執筆した。
  * http://tsukaman.hateblo.jp/entry/2017/12/02/074052
  * 発表内容は上記記事をベースにしている。 
  * 記事内容
    * rootユーザーで作業は行わない。 一般ユーザーで実行。
    * virtualenvを使う。
    * ホストOSにRancherOSを使う。

#### ▷ 「エンプラ&金融系PJの運用保守チームにAnsibleを導入してみた」 @tarosaiba

[資料](http://www.slideshare.net/taroshun/3ojisanansible)

発表が面白くて全然メモ取らなかった。資料を参照のこと。

#### ▷ 「AnsibleとAWXでレガシーな本番環境デプロイを1-Click実行」 @innossh

[資料](https://speakerdeck.com/innossh/lt-ansible-night-in-tokyo-201712)
