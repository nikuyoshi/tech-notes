---
title: "AnsibleFest2018"
date: 2018-10-02T09:05:12-05:00
draft: true
---

# AnsibleFest2018

## State of Automation & Ansible Updates (1日目)

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

https://www.slideshare.net/JrgenEtzlstorfer/selfhealing-applications-with-ansible

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

## Automation Stories (2日目)

### Richard and Chad Davis(DevOps Manager - Service Master)

Richardさんの話が聞き取れず辛かった

* レガシーなシステムを変えていった
* Microservice、DevOpsに変更して戦略を変えた
* 2時間かかっていたものがAnsible Playbookを使うことによって10分に短縮された
* ChatOpsで自動化

### Richard and Jason Cumings (Systems Engineer in US Bank)

Richardさんの話が聞き取れず辛かった。

* ビジネスにおいてDevOpsをする重要性は何か？
  * レガシーなシステムを変えてスピードを出す必要があった
* どのようにして技術的な革新を広めていったか
  * 小さく始めた。
  * Shell ScriptからChefに移行したが、コストがかかった。 Ansibleはモジュールがあるので学習コストが低く抑えられた
* Kubernetesといったコンテナ基盤を使うにあたってAnsibleを使う？
* 次に革新を起こそうとしていることは何か？

## Ansible Best Practices: Roles & Modules

by Tim Appnel (Senior Product Manager)
一、二を争う良いセッションだった

### Self-introduction

Bank Americaの教育に携わっていた？

### Ansible way

* Ansibleはスイスアーミーナイフのように鋭く切れる武器である
* Ansibleのジョブを作成するのに、RoleとModuleを使い分けること
  * Roleはベストプラクティスに則って作成する。再利用性を重視。
  * Moduleはツールである。

### Best Practices

#### Role

* YAMLのシンタックスに則ること
* Gitといったバージョンコントロールシステムで管理すること

#### Role Design

* 設定とアプリケーションの
* Roleはクラス、オブジェクト、ライブラリじゃない。 依存はなるべくさけるとのこと。
* Kepp Roles loosely-coupled
* EXHIBIT AとEXHIBIT Bという具体例とを比較して、EXHIBIT Bの方が疎結合で出来上がっているので良いとの話をしていた。
* モノリシックなRoleは避ける
* `ansible-galaxy`コマンドを使ってRoleをインストールすること。`requirements.yml`を使って依存関係を定義する。
  * 今のやりかたで良さそう！！
* webserverのEXHIBIT A、EXHIBIT Bの例
  * 適度にRole Variableを設定すること
  * `defaults/main.yml`でデフォルトのVariableを適度に設定しておくこと
* Roleのテストをするにはmoleculeを使うこと
* ansible-lintを使っていくこと
* commandモジュールをなるべく使わない
  * 使うことが多いならモジュールを作成しよう！！

#### Module

* モノリシックな、何でもできるモジュールはよくない
* 何度実行しても副作用のないように実装する
* Fail fast - 失敗したらすぐに検知して失敗したことを報告する
* 依存関係は最小にする
* モジュールのインターフェースはアクションやコマンドパラメーターを避けること
* パラメーターはスネークケースで、小文字。
  * フラットな階層のパラメーターであること
* よく使われるようなパラメーター名を使うこと 
  * name
  * state
  * dest
  * src
  * path
  * username
  * password
* モジュール実装で比較したいもの
  * kubernetes
    * モノリシック。Kubernetesの知識が必要
  * ansible-kubernetes-modules
    * 自動生成されたAPIマッピング
  * k8s
  * k8s_scale
* モジュールが返答すべきこと  返り値に一貫性をもたせること
* 参考になるいいモジュール
  * sysctl
    * ベストプラクティスに則ったモジュール。とても良い
  * ping
  * cron
  * get_url
* Developer Guideも参考になる
  * https://docs.ansible.com/ansible/devel/dev_guide/

## Simplifying playbooks

by Jon Hawkesworth (Software Engineer at M*Modal Ltd)
独自テクニック、例えばPlaybookをシンプルにするのにShellモジュールを使うなど、ベストプラクティスからほど遠い話で正直聞かなくても良いセッションだった。 ただし、リストからディクショナリい変換するやり方など、Ansibleでゴニョゴニョしなきゃならない箇所は参考になりそう。

* 経歴
  * サポートエンジニアから開発者へ
* M*Modalについて
  * 世界中にあるデータセンターを利用している。オンプレミス。 
  * Windowsサーバーがほとんど。
  * Dev、Data center、サポートチームがあり、たくさんの成熟したテクノロジーを利用している
* `when:`は必要な時だけ使うべき。複雑になる。

### プロビジョニングするものとアップデートするPlaybookを一つにすること

* リストをディクショナリに変換するやり方

## Developing Ansible Automation with the Galaxy Ecosystem Toolchain

by Chris Houseknecht(Galaxy Engineering Manager at Red Hat)

### Galaxy 2.0

* EC2の上にホスティングされていた
* GitHubに密結合

### Galaxy 3.0

* UIの改善
* データモデルを改善し、ネームスペースが導入された
* OpenShiftにホスティングされた
* Mazer ... Ansibleのコンテンツマネージャー
* 検索の精度があがり、キーワードにマッチするようになった。

### Galaxy 3.1

* ホストされたコンテンツ
  * Checksum
* コンテンツマネジメントがMazerでできるように
* モジュールとプラグインも使えるように
* 開発のワークフローができるように
  * anisble-lintやmoleculeとの連携
* 品質のスコアリングができるように
* 解析ができるように

### Galaxy 3.1 Hosted Content

* GitHub、TravisCIを経由して成功したものをGalaxyがpullしてきた
* 今までGitHubに依存してきたものを他のSCMでも代替できるようになった

### ArtifactとBuildのデモ

galaxy.ymlにキーワード

`mazer build` を実行するとtar.gz ができあがる。メタデータがその中に含まれる。 その後、
`mazer publish ./releases/foo.foo-0.0.1.tar.gz`を実行する

* 個人で作ったRoleはpulpというコンテンツマネージャを使うと良いらしい
  * https://github.com/pulp/pulp_ansible

### Module & Plugins

`ansible-galaxy init`で作成されたフォルダに、Pythonのモジュール(`/library`)などが追加される。
`molecule init`でCollection？が作れるらしい

### Ansible Contentのデモ

https://galaxy-dev.ansible.com/

### Molecule

* molecule init collection
* molecule init role
* molecule init scenario

などそれぞれのコマンドを使い分けること

### Mazerのデモ

https://github.com/jctanner/MAZER_DEMO

## Ansible + VSCode: Accelerate Ansible Playbooks

* VSCodeの拡張の紹介。
* 自動で補完してくれる
* デフォルト設定で動かないのはなぜ？
  * yaml拡張子をVSCodeのAnsible Pluginが認識できるような設定にしないとダメみたい。

### Playbookをスクラッチで作るデモ

### SSH経由でリモートのコンテナのマシンにAnsibleを実行するデモ

## Managing RHEL with Ansible Roles

by Trey Prinz (Account Solutions Architect at Red Hat)
by Till Maas (Senior Software Engineer at Red Hat)

### Overview of Ansible Roles

* `ansible-galaxy init --init-path ./roles webserver` でRoleを作成する
* `defaults`の変数は最も優先度が低い
* `files`, `templates`ファイルはRoleによってデプロイされる。
* `ansible-galaxy install `でRoleをインストールする

### Overview of RHEL System Roles

* NetworkのRoleがあり、Network Managerを設定している

#### 目的

* eth0のDHCP
* WebBondのボンディング 

#### ドキュメント

https://linux-system-roles.github.io/

## Closing Remarks & Toast

by Tim Cramer

## テルストラ(オーストラリアの通信会社)のAnsible事例 3日目

Michael J Stephens at Red Hat
AARON EISLER at テルストラ

ナショナルチームにいる。ボスから指示があって、自動化が進んでいる。
400人のエンジニアがいる。 
全体としては36billionのRevenue
9billionのrevenue
複雑なシステムを管理している。銀行、公共といったものが顧客としている。
リテール、テレコム、ビシネスのチームに分かれている。
工場系にソリューションを提案することが多い。


### 自動化はフルスタックオートメーションを進めていったのか？

買収で会社が大きくなっていった。その会社のcapabilityを強みを活かしていった。
グローバルに貢献を生かしていった。
ネットワークが肝。アプリケーションの買収をしていった。
ARを使ってどこに何を設定すべきかを可視化した。アプリケーション開発者は可視化に、インフラチームはAnsibleで自動構築するようにしていった。
のりのようにAnsibleを使っていったとのこと。
標準化のしすぎはしないようにして、過剰にルールを作りすぎない。イノベーションが起こりにくくなるため。

### アプリケーションチームとインフラチームとをつなぐにはどうしたか？

* DevOpsを利用してつないでいった。
* いつも挑戦していった。 Playbookを一つの小さい単位で作っていった。
* ネットワーやOSなどのクレイヤーごとに作成して、それぞれをつなぎ合わせていった。
* 大事なことはやりたい作業をできること。
* レゴブロックのようにつなぎあわせていった
* レゴのように城を作ったりマンションをできるが、一つ一つの部品は小さく

* ベアメタルのようなサーバーもAnsibleを使って自動構築のサポートをしている。 by Michael
* AT&T Integrated Clabは90%以上の作業をAnsibleによって自動化している
* 2週間程度でパイロットレベルのものができた。
  * インフラ構築、スイッチ状態の確認ができた。
  * コンフィグ設定を1工程あたり3秒で確認できるようになった
  * Agent less
* API Managementをきちんとしていて、3Scaleといったものを利用して管理している
  * ディシジョンマネジャーを利用している。BRMS。
    * ルール管理をしている。
  * コンテナ上で実現。

### インフラとアプリケーション開発を

* 自動化チームを作成する。
* ネットワークとIT
* テルストラさんもまだサイロは残っている。
* 組織のリストラクチャーが起きている
  * ネットワークとインフラチームが一つ
  * CTO(Chief Technology Officer)とCIO(Chief Infrastructure Officer)を一つにし、CTIOにすることが大事。
  * インフラはデータが持っているが、ネットワークを持っていないため、それぞれのチームを一つにする
  * 1/3の人がリストラされている。
  * CTOにいくまで13階層まであったが、6階層にすることでフラットにして風通しを良くした
* 自動化チーム
  * ハイブリッドチームにすること
  * 専任舞台をしている。アーロンさんのチーム。
  * ガバナンスを効かせる。
  * リバレッジモデル。
  * チャンピオン、ヒーローといわれるAnsibleを使える人を作って、そこからアーロンさんに質問が飛ぶようにしている
  * 全員がAnsibleを使えるようにしたいが、現時点ではそうなってる。
* 人とプロセスとテクノロジーを使って文化を変えるのが大事。
* 一つのプロジェクトをDevOps、アジャイルで変えていくのが大事。
  * そこから成功体験を感じることが大事
  * 小さいところから始める。そこが大事。

### レガシーなシステムから移行するために、初期コストもかかるが、どのようなところからAnsibleを小さくから適用していったか

* 像をまるのみせずに少しずつかじることから始める
* オートメーションとオートマティック
  * オートマティックは、人間が触らずに0タッチ
  * オートメーションは、徐々に自動化を進めていく状態のこと
* ヘルスチェック、維持管理からまずはPlaybookから起こす
* その後にレポートを作成するようなPlaybook
* 最後にメールを起こすPlaybookといったようにブレイクダウンしていった。

* 今までコストを落とせるか
* 投資回収は1ヶ月くらいでできてしまうのでやってしまったほうが良い。
* データセンターは20週間で行っていたことを2週間でできるようになった。
* コンサルティングや設計は同じ工数だが、開発、ビルド、配信は20%以上削減できた。

### ルーターといったネットワークの設定を変更するにはどのくらいのコストがかかったか

* docomoはSIを使って、2週間で2つのルーターに10万円かかっているらしい。

### Playbookは

### CI/CDをどのようにしているのか

* アプリケーションチームはZuul、Jenkinsを使用している。
* インフラチームはAnsible
* 現場がやりたいと言っているならやらせているとのこと。
* Jenkinsと複数組み合わせてジョブでまわす