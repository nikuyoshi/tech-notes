+++
title = "AWS CLI"
+++

## 全リージョンに対してあれこれするスクリプト

以下の例は全リージョンのEC2リストアップのスクリプト。 `aws ec2 describe-instances` の箇所を適宜変えれば全リージョンに対してまとめて実行できるスクリプトとなる。

```
for region in `aws ec2 describe-regions | jq -r ' .Regions[].Endpoint | match("^ec2.(.+).amazonaws.com") .captures[].string'`
do
     echo -e "\nListing Instances in region:'$region'..."
     aws ec2 describe-instances --region $region | jq '.Reservations[] | ( .Instances[] | {state: .State.Name, name: .KeyName, type: .InstanceType, key: .KeyName})'
done
```