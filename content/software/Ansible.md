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

