+++
title = "Ansible"
+++

## `/var/log/intstance_1`, `/var/log/instance_2` のようなシーケンシャルなパスを変数に格納したいとき

```
- name: Set fatcs
  hosts: localhost
  sudo: no
  connection: local
  vars:
    instance_number: 4
  tasks:
    - name: Register instance's sequential path
      set_fact: 
        instance_path: /var/log/instance_{{ item }}/log
      with_sequence: start=1 end={{ instance_number }}
      register: sequential_path

    - name: Register instance's sequential path list
      set_fact:
        instance_path_list: 
          "{{ sequential_path.results | map(attribute='ansible_facts.instance_path') | list }}"
        
    - name: debug
      debug: 
        var: instance_path_list
```

実行結果結果

```
TASK [debug] **************************************************************************************************************************************************************************************************************************************************************************************************
ok: [localhost] => {
    "instance_path_list": [
        "/var/log/instance_1/log",
        "/var/log/instance_2/log",
        "/var/log/instance_3/log",
        "/var/log/instance_4/log"
    ]
}
```

## Ansibleのコーディング規約について

### 変数名

[OpenShift][1], [edX][2]のコーディング規約を参考にして、以下のとおりに変数名を設定することにした。

* Role変数はRole名を先頭につける。
  * Role名は、OpenShiftのように、省略形をつけるのではなくロール名をまんまつけること。他のRoleとバッティングすることを避けるため。[3]
* ロール内に閉じた変数であれば、先頭に`__`をつける。

その他コーディング規約で意識することができたら随時追記予定

[1]: https://github.com/openshift/openshift-ansible/blob/master/docs/style_guide.adoc#role-name-prefix-conflicts
[2]: https://openedx.atlassian.net/wiki/spaces/OpenOPS/pages/26837527/Ansible+Code+Conventions
[3]: http://tdoc.info/blog/2014/10/09/ansible_coding.html