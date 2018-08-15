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
4. rebaseされたコミットがRemoteにあった場合、ローカルの変更履歴をstashするなりしてから`git branch -B master origin/master`のようにリモートブランチと同期を取る。
   * 参考: [How can I extract a predetermined range of lines from a text file on Unix?][1]

[1]: https://stackoverflow.com/questions/83329/how-can-i-extract-a-predetermined-range-of-lines-from-a-text-file-on-unix
