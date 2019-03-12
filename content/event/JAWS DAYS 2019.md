# JAWS DAYS 2019

## AWSのManagement Toolsを使ったハイブリッドアーキテクチャ

対象者はAWSomeDay、Technical Essentials1受講済みレベルを想定。
Transit Gatewayを利用すれば、ルーターとして利用できるため、VPCとVPN、Direct Connect間を快適に結べる。

AWSのエージェントについては中から外に対しての通信しかしていないのでセキュリティ的に安全ですよ

SessionManager ... サーバーにログインせずにインタラクティブに操作できる。サーバーでの操作ログを記録できる。
Raspberry Piもエージェントを仕込めばAWSから監視できるよ！！

S3にAnsible PlaybookやShell Scriptを置いておけば、SystemsManagerのRunCommand経由でオンプレに対してコマンドを実行できる。
CloudWatchでOSメトリクスを収集&監視できるようになった。 CloudWatchの統合エージェントを導入すれば、OSのメトリクスを情報収集できる。
ただし課金されるので注意。

Systems ManagerのRun Cpmmandについては、Black Belt資料を参考にすること。

CodeDeployはインターネットに一度でないとダメ。

## クラウド時代のモニタリングといえばDatadogだよね

Cloud Functionsで、サーバーレスのサービスも簡単に監視できる
コンテナモニタリングで、Kubernetesの利用が多い。
Fargateモニタリングは増加傾向。
ECSではDockerレジトリに公開されているイメージはあまり使われていない。カスタムアプリケーションの用途がメイン？

[8 emerging trends in container orchestration](https://www.datadoghq.com/container-orchestration/)

コンテナの負荷状況を一覧表示できる

Sysntetics - 外形監視もできるようになってきてる。

## ハンズオン

1. Amazon LightsailでWordpressを構築しEC2へマイグレーションを実行
2. AWS CognitoとIAMで認証認可を学び、S3バケットへの権限制御を試す
3. Amazon API GatewayとAWS Lambdaを活用してAmazon Dynamo DB へRESTインターフェースでデータ操作を行う

### Lightsail利用上のTIPS

VPC Peeringにより既存ネットワークへのアクセスが可能。デフォルトはVPCのみ
下り通信費用が固定、かつ低価格。 1TB = 3.5USD/Mo. EC2の場合は、1TB = 116.74USD

### IAMの違い

IAM ユーザー、ロール、ポリシーそれぞれの違いを説明。

ユーザー: 管理者に付与する管理権限
ロール: リソースに付与する管理権限
ポリシー: ユーザー、ロールに付与する権限制御パラメータ

### Cognito User PoolsとIdentity Pool

User Pools: ID/PWDの管理サービス
Identity Pools: User Poolsのユーザーに対して権限付与。IAMとの関連付け。

### Lambda

セキュリティの問題があった場合に、Lambdaで使える

### API Gateway

REST APIをホスティングできる基盤。

## 気づき

* 一方的に話すのではなく、適宜問いかけを5分に1度ペースくらいで設ける。
  * JP1といったよく知られた製品等を例に挙げて話をすると理解が促進されるので、製品知識もあるとなおよし
* ざっと幅広い情報を提供して、深掘りしたい場合は資料を読んでもらうように案内。