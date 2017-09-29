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

## 参考

[How to get the start time of a long-running Linux process?](https://stackoverflow.com/questions/5731234/how-to-get-the-start-time-of-a-long-running-linux-process)