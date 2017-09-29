+++
title = "ShellScript"
+++

## Tips

### 進捗状況を表すバー

```bash
while [ 1 ]; do echo "test"; sleep 1; done | pv > /dev/null
```

`echo` している部分を処理に置き換えれば進捗状況を表示できる。

### デバッグログ出力方法

bash 4.1以上にてスクリプトの先頭に次のように書いておく

```bash
#!/bin/bash

exec 5> debug_output.txt
BASH_XTRACEFD="5"
PS4='$LINENO: '
set -x
```

するとdebug_output.txtにログが出力される。