+++
title = "Linuxコマンド"
+++

## プロセスの起動時刻を調べたい

```shell
$ ps -eo pid,cmd,lstart
  PID STARTED                      ARGS
    1 Tue Sep 19 13:06:32 2017     /sbin/launchd
   50 Tue Sep 19 13:06:34 2017     /usr/sbin/syslogd
   51 Tue Sep 19 13:06:34 2017     /usr/libexec/UserEventAgent (System)
...
```

## カレントディレクトリ配下の複数ファイルの拡張子を一括置換したい

以下の例は、拡張子を`heic`から`jpg`に変換するワンライナーである。
`echo mv`とやると、ドライランで実行できる。表示を確認してから`echo`を外して実行すれば安全。 

```sh
$ for file in *.heic; do echo mv "$file" "${file%.heic}.jpg"; done
mv IMG_0808.heic IMG_0808.jpg
...

--- 出力確認後、echoを外す ---
$ for file in *.heic; do mv "$file" "${file%.heic}.jpg"; done
```

[参考ページ:mac os x terminal batch rename](https://stackoverflow.com/questions/24102974/mac-os-x-terminal-batch-rename)

### 参考

[How to get the start time of a long-running Linux process?](https://stackoverflow.com/questions/5731234/how-to-get-the-start-time-of-a-long-running-linux-process)

## SSHで一度ログインしたら二度とパスワードを入力しなくて済む方法

前提として、インターネットから隔離されたネットワークでSSH接続をする際に毎回パスワード入力を強いられる時を想定している。
秘密鍵認証は関係ない。

手順

1. `ssh-keygen`で秘密鍵を生成する
2. `ssh-copy-id ユーザー名@IPアドレス`で秘密鍵をリモートに転送する 
3. `ssh ユーザー名@IPアドレス`でパスワード抜きでログインできるか確認する
4. 1-3を実施しても駄目なら`ssh-add -K /path/to/private_key` を実行する 

毎回新しいホストに対して手で設定してられないので、以下のシェルスクリプトを任意の場所に置いた上で、~/.zshenvでsshのエリアスを設定している。

```bash
#!/bin/sh
ssh-copy-id $1 1>/dev/null 2>/dev/null; ssh $1
```

```bash
# ssh
alias ssh=~/sh/ssh-auto-login.sh
```



### 参考

[Using an ssh-agent, or how to type your ssh password once, safely.](http://rabexc.org/posts/using-ssh-agent)

> 1. Generate a set of keys, with `ssh-keygen`.
> 2. Install your keys on remote servers, with `ssh-copy-id`.
> 3. Start an `ssh-agent` to use on your machine, with eval `ssh-agent`.
> 4. `ssh-add` your key, type your password once.
> 5. Profit! You can now ssh to any host that has your public key without having to enter a password, and use `ssh -A` to forward your agent.

[SSH Key - Still asking for password and passphrase](https://stackoverflow.com/questions/21095054/ssh-key-still-asking-for-password-and-passphrase)

> `ssh-add -K /path/to/private_key`