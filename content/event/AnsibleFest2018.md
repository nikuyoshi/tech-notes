---
title: "AnsibleFest2018"
date: 2018-10-02T09:05:12-05:00
draft: true
---

# AnsibleFest2018

## State of Automation & Ansible Updates

### Michelle Perz

* 今回のイベントで1000人超え
* 今回から2日のイベントに。
* パーティが6-9PMに実施される。

#### トラック

* ASK AN EXPERT 
  * 3階で実施。
  * `#ASKANSIBILE` のハッシュタグも
* GETTING STARED

### Justin Nemmers

* STATE OF AUTOMATION
* ツールが増えて複雑になってきているが、Ansibleではシンプルに管理ができるよ！
* 自動化することでツール、変化や複雑性を管理できるようになった
* データベース、OS自動化に加えてセキュリティに関する自動化も新しい焦点として行うようになった
* インフラ、ネットワーク、IT OPS、DevOps、セキュリティに関してチームの開発を加速するAnsible。
* 2016年から2018年にかけてモジュールが500から2000に増えた。4倍！！
* Red Hatが自動化について保証をする。

### Harry Karr

TIAAという金融会社の事例

* Ansible Towerによって効率化できた事例
* コードレビューを行うことで品質を保証できるように。

### Justin Nemmers

* Ansible Galaxy
* Ansibleを利用すれば、自動化を加速でき、問題を解決できる。 

### Jason McKerr

Ansibleの方針を決めている人。

* Ansible Engineでは3つの戦略を注力している。
  * パフォーマンス、スケールアウトをすること
  * GCEといったクラウドに関連するモジュール、ネットワークの管理をできるようなモジュールの強化
* Ansible Towerでも同様に3つ(スケーラビリティ、アクセス、コンテント)の方針をとっている
* RHEL、OpenStack、Openshiftといったハイブリッドの環境に対しても自動化dけいる。
* セキュリティの自動化に関しても焦点をあてて取り組んでいる
* セキュリティの自動化として、
  * リスクアセスメント
  * Threat 
* Ansibleによって、チームをまたいだ自動化をできる。

### Iftikhar Khan

* Ansibleによってネットワークエンジニア、ネットワークオペレーター、ネットワークセキュリティなどの各チームを一つにできる
* ただし、SDN、HOST NETWORKING、ネットワーク仮想化、CONTROL PLANE、DATA PLANEは含まない。
* 含むのは、OPERATION、AUGMENTATION、CONSUMPTION、SIMPLIFICATION。
  * CONSUMPTIONって何？ 
* 50のネットワークプラットフォーム、700以上のモジュール、12以上のネットワークのロール
* ネットワークのビルトインモジュールの一例。 30以上！！
* ネットワークだけでなく、セキュリティ、クラウド、DevOpsなど多方面でも自動化の機能を提供してるよ！！
* VPNのマルチクラウドでの活用事例も聞けるとのこと。

### Robyn Bergeron

Ansibleのコミュニケーションアーキテクト

* AnsibleコミュニティにおけるコントリビュートがAnsibleをより大きく、良いコミュニティになる
* Ansibleコア、AWS、Ansible Galaxy
* 12987のフォーク、32800のスター、4万のコミット
* CONTRIBUTORS SUMMITが6回目がある。
* 243のミートアッグループ、、、
* AWS、Windows、VMware、Azure、Networkに関連するワーキンググループコミュニティがある。
* Ansible GalaxyのRoleが17.9K。NGINXのRoleが1100以上。なぜこんなに多いの。。。
* ansible-lint、Molecule、Zuulといったコミュニティとも連携。
* 「一番良いアイデアはコミュニティから来る」「コミュニティは力を増強させるもの」と言っているくらいコミュニティを大事にしている

## Tool Overload! Where Does Ansible Fit?

### 筆者について

* 自動化に関連する技術を10年以上経験してきた
* Ansibleに関しては3年近く経験がある。
* Homebrewのパッケージを

### Kovarusについて

* 本社はシリコンバレーにある。
* システムインテグレータ。14年以上のリードをしてきたとのこと。
* アプリケーションのデリバリ、クラウドのインテグレーションなどのサービスを提供

### Brief Overview of Ansible

* 開発が始まってから6年
* Ansible(OSS版)とAnsible Engine(サポートあり)
* AWX(OSS版)とAnsible Tower(サポートあり)

### AnsibleのPros And Cons

* Pros
  * エージェントレス
  * すぐに始められる
  * プラットフォームのサポートが広い
  * オープンソースのGUIDINGがある。AWX
* Cons
  * デフォルト設定だと遅い
    * タイムアウト設定など
    * 並列実行できる設定はあるが、デフォルトだと遅いよね
  * Isn't very stateful
    * AWSなどのインスタンスを作成するPlaybookだと、毎回10個作成しちゃって辛い、など

### どのような箇所で使えるか

#### Orchestration vs Configuration Management

* Orchestration
  * Inherently Procedural
  * Involves sets of 

#### Ansible is unique

* Ansibleであれば設定管理やオーケストレーション両方ともひとつのコードで管理できる。

#### DevOps Tool chain

https://www.zdnet.com/article/atlassian-packages-tools-to-help-enterprises-accelerate-devops-adoption/

* Ansibleはビルド時に活躍する
  * ビルドスクリプト代わりになる
* CIにも使える
  * https://www.atlassian.com/devops
  * インテグレーションやインテグレーションテストにも使える
* デプロイにも使える
  * コンテナの作成
  * クラウドのインスタンスの立ち上げ
  * アプリケーションのアップグレード
* オペレーションにも使える
  * 障害からの自動復旧
  * 監査
  * by Ansible Tower...
* ネットワークの自動化
  * ネットワークの自動化にはAnsibleがむいている
  * 40以上の異なるネットワークプラットフォームのサポート
  * 570以上のネットワークモジュール
  * Ansible Galaxyのネットワークサポート by Kovarus

* Ansibleのサポートが必要なもの 
  * バージョンコントロールの管理
  * ライフサイクルの管理
  * クラウド管理プラットフォーム
  * インベントリーの管理システム
* Ansibleを適用するのにどこから始めれば良いか？
  * まずは測定すること
  * 小さいところから始める。 特に、brown field deployments？から
  * システムの主となる箇所から
  * 場所やOSのカーネル、種別に応じたプラットフォームごとにグルーピングする。
    * ジュニパーやCiscoなど
  * セキュリティ監査
  * CMDBのバリデーション
  * Ansibleのエバンジェリストを雇う

### サマリ

* Ansibleは幅広く適用でき、アクティブなOSSコミュニティがある。
* Ansibleを使用したいならすばやく始められる
* 幅広いプラットフォームのサポート

### 質問

* Puppetと比較してどうか？
  * Puppetは言語を学ばなければならないし、プラットフォームのバグも自分たちで直さなければならない
  * オーケストレーションの変更の対応がAnsibleの方が容易。
* AnsibleのKickstartingとして何がいいか？
  * Cloudformsが良い。


## Make your Ansible Playbooks Flexible, Maintainable, and Stable

立ち見が出るほどの人気。
AcquiaのDeveloper

* How did you get started with Ansible?
* How long have you been using it?
* What's your favorite thing to do when you Ansible?

### Hosted apache solr


### Drupal VM & Mac deb playbook

* 複数のPCのキッティングをするのにChefだと時間がかかっていた
* Ansibleを使い始めると、それぞれの設定をAnsibleで管理していたため、差分を適用するのに便利だった。

### Media E-commerce　platform

### 学んだこと

* 整理整頓することを続けること
  * コミットメッセージも
  * ビルドサーバーからPlaybookを常に実行する
* 「大事なことは人は忘れてしまうことだ」
  * READMEをきちんと書くこと
    * Purpose
    * Links(CI, Docs, issue tracking)
    * Instructions for local testing
* 小さいファイルを心がけること
  * 一つのファイルで100行以下
  * "include_*" を使った関連タスクにしておくこと。
  * 一つのロールに対して一つの責任だけを負わせるようにしておくこと。
* Roleについて
  * ジェネリックなロールにしておくこと
  * プロジェクト間でロールを共有すること
  * Ansible Galaxyから使う、GalaxyにRoleを提供すること
    * requirements.ymlから依存関係を解決する。 → 今までやってきたことは間違ってなさそう
* Testについて
  * 頻繁に行うこと
  * Ansible CI Spectrum
  * 以下の下になればなるほど複雑になる
    * yamllint
    * ansible-playbook --syntax-check
    * ansible-lint
    * molecule test(integration)
      * https://molecule.readthedocs.io/en/latest/
    * ansible-playbook --check(against prod)
    * Parallel infrastructure
* 注意したほうがいいこと
  * Deprecationの警告に注意すること
  * Porting guidesに目を通すこと
  * あまりにもうっとおしいWARNメッセージをdisableすること
    * commandモジュールのargs: no
  * CI環境を常に最新にすること
  * Ansibleの最新版をターゲットにすること

### Simplify, optimize

* Airpodsの例をあげて、シンプルさが大事なことを伝えていた
* "YAML is not a programming language"
* flat variableを使う

×
```
apache:
  startservers:2
```

○
```
apache_startservers:2
```

* スピードの効率化
  * 不必要なら `gather_facts`を使わないこと
  * `forks`設定を可能な限りリソースを使うような設定にすること
  * もし遅いならCIをしないこと
* モジュールに関連すること
  * package
  * copyモジュール - シングルファイルに対してのみ使う。 もしくは小さいディレクトリ。
  * lineinfile - 
* `ansible.cfg`に`callback_whitelist`を設定すること


## Self-healing applications with Ansible

* 自動復旧をするのにAnsible Towerを利用して実現した。
* dynatraceで障害を検知して、復旧させる箇所でAnsibleを利用している
* 自動復旧するアプリケーションを作るには？
  * まずは監視をするところから始める
  * runbooks 経由で自動化する
  * 小さいところから始める。
    * 頻繁に起こる問題は何？
  * 小さいところから初めて、自動化を広げていく。
  * 文化も変えていく

## Database Automation with Thousands of database, monitoring and backup

LINEの事例。

* AWSは使っていないとのこと
* データベースは1万超え
* 社内ではMySQLは82%以上使っている。Redisも使っているとのこと。
* MySQL Enterprise Backupを3.10から3.12にアップグレードするミッションが2016年にあった。
  * 3000以上あるサーバーに簡単にデプロイできる方法を模索していた。
  * 今までは簡単なシェルスクリプトを試していた
* Chefなどの別のツールも使っていたが、簡単にデプロイできるということからAnsibleを採用した
* Ansibleで並列でインストールをした結果、リニアに実行時間が増えずに、logN程度くらいに小さくなった。
* 複数のDatabaseを監視するソリューションがなかったため、DBONEというシステムを作成した。
  * https://www.slideshare.net/linecorp/dbone
  * Ansibleは、PrometheusやGrafanaといったOSSのをインストール、アップグレードする際に利用した。

### Q&A

* MySQLのインストールモジュールは自作のモジュールか？
  * Ansibleモジュールを利用して開発したとのこと

## Building Automation Teams in Today’s Organizations

* Payal Singh
* Jason Lamb
  * Intelのエバンジェリスト
* Walter Bentley
  * ○○会社のVice President
* Carlos Caicedo
  * Syracuse UniversityのAssociation Professor
* William McKenzie
  * ソリューションアーキテクト。自動化導入などに関与。

### 自動化によって組織にどのような影響を及ぼすか？

* Payal Singh
* Jason Lamb
  * ハイブリッドクラウドにも対応できるようになる?
* Walter Bentley
  * 時間(工数)が変わる。マインドセット。
  * 文化が変わる。
* Carlos Caicedo
* William McKenzie
  * 

### チームにAnsibleを使ってもらうのにどの程度時間がかかったか

* Payal Singh
  * 
* Jason Lamb
  * 
* Walter Bentley
* Carlos Caicedo
  * 
* William McKenzie

### 自動化するエンジニアにとって必要なものは？

* 新しい技術を学ぼうとする姿勢、情熱
* ジェネラリスト

### 何を自動化したいか

* アクションアイテム
* ドキュメント

## ASK THE EXPERT

Ansible Roleのcommon roleについて聞いてみた。結論としては、common roleによせるべきタスクはタスクが2回以上使われるようなケースで、ケースバイケースなことが多いとのこと。

