---
title: "Git"
date: 2018-08-15T15:46:30+09:00
draft: false
---

## 個人プロジェクトのGitについて

一人しか操作する人間がおらず、複数端末でPushするユースケースがほとんどのため、以下のことに留意する。

1. 修正したファイルがあれば、こまめにコミットする。
2. ローカルにある程度コミットが溜まってきたら、`git rebase -i`でコミットをまとめる。RemoteにPushしたコミットでも、まとめたほうが良いものがあればrebaseして綺麗にしておく。
3. 履歴をまとめる際、一般的に`git fetch; git merge --squash`の方が安全だが、どうせ個人でしか使わないので昔の履歴を追いやすい形にしておきたい。
4. rebaseされたコミットがRemoteにあった場合、ローカルの変更履歴をstashするなりしてから`git checkout -B master origin/master`のようにリモートブランチと同期を取る。
   * 参考: [How do I reset 'master' to 'origin/master'?][1]

## Git Submoduleで管理していたリポジトリ名が変更されたとき

下記の通りに一旦削除して、`git submodule add`してあげればOK。

```
0. mv a/submodule a/submodule_tmp

1. git submodule deinit -f -- a/submodule    
2. rm -rf .git/modules/a/submodule
3. git rm -f a/submodule
# Note: a/submodule (no trailing slash)

# or, if you want to leave it in your working tree and have done step 0
3.   git rm --cached a/submodule
3bis mv a/submodule_tmp a/submodule
```

[How do I remove a submodule?][3]

## 困ったときに参考になるサイト

[Gitでやらかした時に使える19個の奥義][2]

[1]: https://superuser.com/questions/273172/how-do-i-reset-master-to-origin-master
[2]: https://qiita.com/muran001/items/dea2bbbaea1260098051
[3]: https://stackoverflow.com/questions/1260748/how-do-i-remove-a-submodule