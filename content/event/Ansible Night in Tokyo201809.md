---
title: "AnsibleNightinTokyo201809"
date: 2018-09-21T19:05:32+09:00
draft: false
---

# Ansible Night in Tokyo 201809

## GitLab で実現する Ansible コードの管理」

by クリエーションライン 荒井裕貴さん

* Infrastructure as Codeのお話
  * 再現性
  * 正確性
  * 透明性
  * 3回以上実行すれば元は取れる

既にGitLabもAnsibleも使っていて、マージリクエストのフローも導入してるので新しく知ることはなかったな。。。

## インフラCI実践ガイド 〜Ansible x GitLab による継続的改善例 〜 自動化の正しさの検証を自動化するには」

by レッドハット　中島倫明さん

* Ansibleで構築した環境をAnsibleでテストを行う。
  * タスクにnameをつけ忘れたらビルドをこけさせることができる。
    * https://github.com/willthames/ansible-lint
    * https://github.com/tsukinowasha/ansible-lint-rules

## LT

### Ansibleの学習環境をvSphereで作ってるお話

https://speakerdeck.com/skyjoker/ansiblefalsexue-xi-huan-jing-wovspheretezuo-tuteruohua

### 「ElasticBeanstalk で Ansible を使っている話」

by @laugh_kさん！

https://www.slideshare.net/laughk/elasticbeanstalk-ansible


### 「マイベストVariables設定場所（異論、反論Wellcome！）」

by @morihaya55さん

https://www.slideshare.net/ssuser1f3c12/ansiblejpbestvariablesplace

* 22箇所も variables を設定できる
  * https://docs.ansible.com/ansible/2.6/user_guide/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable
  * group_vars, host_vars ...

* 10数個のrole変数ならInventoryに書き込んだ方がシンプルになる！！

### 「Ansible deploys Istio on kubenetes environment」

by @ichigo_abcさん

https://www.slideshare.net/ssuserd394af/ansible-deploys-istio-on-kubenetes-environment