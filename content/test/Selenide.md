+++
title = "Selenide"
+++

Seleniumのラッパーライブラリ。 Seleniumをより画面のテストをしやすくしたものだと思ってよい。
Javaを使用していて、jQueryの書き方を知っているのであれば導入の敷居は非常に低い。 
とあるID属性が表示されるまで自動でsleepして待ってくれるのも良い。 また、テストがこけた時に自動で
スクリーンショット、およびHTMLを保存してくれる。 

公式のクイックスタートを読めば何ができるのか大体分かる。 
http://selenide.org/quick-start.html

Seleniumとの比較も公式ドキュメントとしてまとまっている。
http://selenide.org/documentation/selenide-vs-selenium.html

## サンプル

1. ログイン
2. 指定した画面まで遷移
3. 検索

を行っている。

```java
import org.openqa.selenium.By;
import org.openqa.selenium.chrome.ChromeOptions;
import org.openqa.selenium.remote.DesiredCapabilities;

import static com.codeborne.selenide.CollectionCondition.size;
import static com.codeborne.selenide.Selectors.byText;
import static com.codeborne.selenide.Selenide.*;
import static com.codeborne.selenide.Condition.*;
import static com.codeborne.selenide.Condition.text;
import static com.codeborne.selenide.Selenide.open;

public class Test {
    @org.junit.Test
    public void ccmTest() {
        String baseUrl = "http://...";
        // Chrome Driverのパス
        System.setProperty("webdriver.chrome.driver", "~/chromedriver/chromedriver");
        System.setProperty("selenide.browser", "Chrome");
        clearBrowserCookies();
        // シークレットモードで起動
        ChromeOptions options = new ChromeOptions();
        options.addArguments("--incognito");
        options.addArguments("--lang=ja");
        DesiredCapabilities capabilities = DesiredCapabilities.chrome();
        capabilities.setCapability(ChromeOptions.CAPABILITY, options);

        // ブラウザ起動
        open(baseUrl);
        // ログイン
        $("#loginId").setValue("id");
        $("#password").setValue("password");
        $("#loginButton").click();
        // 画面遷移
        $(byText("link1")).click();
        $(byText("link2")).click();
        $(byText("link3")).click();
        // タブがポップアップされるため、タブ切り替え
        switchTo().window(1);
        // 画面遷移
        $(byText("hoge")).click();
        $(byText("fuga")).click();
        // 検索
        $("#searchButton").click();
        // 検索後一つ一つの画面項目が想定通りに表示されているかチェックする
    }
}

```

## 参照

* [mybatis/jpetstore-6](https://github.com/mybatis/jpetstore-6/blob/master/src/test/java/org/mybatis/jpetstore/ScreenTransitionIT.java)
* [Effective UI tests with Selenide](https://asolntsev.github.io/en/2015/12/31/selenide-at-advent-calendar/)