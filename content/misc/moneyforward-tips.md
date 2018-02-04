+++
title = "MoneyForwardのTips"
draft = false
+++

## MoneyForwardのTips

### CSVファイル一括ダウンロード

ログインした状態で以下のソースコードをChromeのDeveloper Tools等で入力する。

```javascript
urls=[];
for(y=2017;y<=2017;++y)
  for(m=1;m<=3;++m)
    urls.push('https://moneyforward.com/cf/csv?from='+y+'%2F'+m+'%2F01&month='+m+'&year='+y);
function doLoop(){
  if(url=urls.pop()) {
    console.log(url);
    var link = document.createElement("a");
    document.body.appendChild(link);
    link.href = url;
    link.click();
    document.body.removeChild(link);
    setTimeout(doLoop,3000);
  }
};
doLoop();
```

### CSVファイルから特定項目のgrep

CSVがSJISになっていて文字化けするので`iconv`で文字コード変換をする

```sh
iconv -f SJIS -t UTF-8 収入・支出詳細_2017* | grep 水道料金
```

特定の項目を計算する

```sh
iconv -f SJIS -t UTF-8 収入・支出詳細_2017* | grep 水道| perl -F',' -alne '{print $F[3]}' | perl -pe 's/"//g; s/-/+/g; s/\n//g;' | perl -pe 's/^\+(.+)/$1\n/g' | bc
```
