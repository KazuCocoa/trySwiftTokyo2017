# Tasting tests at Cookpad
`@Kazu_cocoa`

皆さんこんにちは。
クックパッドでテストエンジニアをしてます松尾です。
今日はSwiftやiOSに関係する人たちの集いで発表することができ、とても興奮しています。

私はテストエンジニアなので、今日の話はテストにまつわるものになります。
ちなみに、このタイトルは私は料理にもかかわる会社に属しているのでtastingとしてみました。

# About me

まず自己紹介です。
私は松尾和昭といい、クックパッドでテストエンジニアやソフトウェアエンジニア in Qualityとして働いています。
私は普段はモバイルアプリのテスト自動化やプロセス改善、もっと大きく組織的な改善活動にも関わっています。
開発言語としてはSwift/Ruby//Java for Android/Elixirに触れることが多いです。
最近、AppiumのRuby bindingをメンテナンスしています。
Appiumは、有名なモバイルアプリのテスト自動化ツールです。

# 😋

では、発表を始めましょう。

# A bunch of topics in tests
"TEST"といっても、数多くのテーマや意味を持ちます。
例えば、usability testやperformanceテストといったカテゴリの話があったり、unit test/integration testといったテストレベルの話であったり。
それらの中で、今日はテストピラミッドと呼ばれるunit testやintegration test、UI testと区分されるテーマに関してお話をします。

# How UI Tests support our development

今日はこの中でUI Testが私たちの何を支えたのか、をtastingしてみようと思います。
unittestやintegration testの話は今日はしません。

そのため、皆さんはUIテストがどれほど私たちの開発を支えているか、その戦略とケーススタディを学ぶことができます。

この話の後、テスト戦略やUIテストの話を自分たちのプロジェクトで考えてくれると嬉しいです

# We should know about the test target
テストの話をする前に、テスト対象に関して説明します。
これからの戦略の話やケーススタディへの理解を手助けしてくれるためです。

そのため、私はクックパッドのiOSアプリを少し味わってみます。

# What is Cookpad?

クックパッドは世界でレシピ共有サービスを行っています

# simularweb.com
simulator.comによると、クックパッドは食カテゴリで世界で最大のWebサイトになります。
現在、私たちは日本やそのほかの地域に対してサービスを提供しています。

# Cookpad for iOS(Japan and Global)
クックパッドの主なiOSアプリには2種類あります。それは日本向けのアプリと、日本以外に向けたアプリです。
これらは成長レベルが異なるので、まだ統合していません。

グローバルアプリは、non-Japaneseのアプリストから取得可能です。

# Cookpad for iOS(Japan)
今日は、この日本向けのアプリを対象に話します。

# Histries for Cookpad iOS App
このクックパッドアプリはすでに5年の時を経ています。その間、UIを複数回大きく変えました。
2013年に大きくアプリを作り変え、2014年にUIをiOS6の頃から変更し、2015、16年と機能をいろいろ追加したり、除いたりしながら試行錯誤してきました。
見た目も変えるのですが、例えば中身もSwiftへと置き換えを進めているように多くのre-write/refactorをコードレベルでも加えています。
ソースコードも順調に増え、今では10万行ものコードが存在します。

# kano-model and Japan market
比較的見やすい品質モデルにkano-modelがあります。このモデルには当たり前品質を魅力的品質の2種類があります。
日本では、この当たり前品質の要求として特に基本的な機能が動作すること、例えば画面遷移ではクラッシュしないことなどの要求が高いです。
そのため、そういうことが当たり前と感じる人が多い傾向にあるようです。(cookpadのレビューと不具合を参考にすると)

# Diachronic Quality for Mobile

diachronic qualityという造語があります。
これは、変わり続ける品質を説明しようとしていることばです。言語学から影響を受けています。
モバイルアプリ、特にサービスとして提供しているアプリは時代の流れに合わせて変化が大きくなるので、この変化し続ける世界においても、先ほど挙げた日本のユーザが当たり前だと感じる明らかな不具合を減らす必要があります。
例えば、iOSだとOSの変化やUIの変化、実装言語の変化といった品質に関わる要素が毎年といっていいほどに変わります。

# Tasting tests😋

では、この環境の中で行ってきたUI Testの話をしていきたいと思います。

# A History for UI Tests for Cookpad Apps

^ このgithubリポジトリは、automated ui testのツール群の成長の軌跡です。
^ 2014年の頃からUI Tests、特にAppiumを使った環境を作っていきました。
^ この間、先ほどのiOSアプリの変化の歴史をこの自動化されたテストによって支えてきました。

#  Why have we implemented  this UI tests?🤔
私たちは、自分たちのサービスが発展し続け、成長し続ける必要があると知っていた。
そのため、モバイルアプリをre-engineeringしていく必要があった。

# どこから手をつけるか?

> Writing unit tests before refactoring is sometimes impossible and often pointless.

^ rewriteやリファクタを推し進める時、高頻度でテストが行われ、それを元に正しいことを確認し続ける環境を持つことは最近では必要だと知っている人が多いでしょう
^ ただ、例えば何も用意していない状態でunit testといったテストコードを書き始めることは難しいです。アーキテクチャも関係してきます。
^ 一方で、unit testのテストをCIとして実施できるようにしなければ、高頻度の修正を将来に渡って実施し続けることは難しくなります。

# Basic strategy for Re-Engineering

^ そこで、まずはテスト対象のアプリを、内部、外部の2つの側面から見ます
^ 内部、とはユーザには見えないソースコードレベルの話です
^ 外部、とはユーザに見えるようなUIが関わる領域の話です

# 内部を変更できるようにするために、外部からカバーしていく

1. コードの内部を変更することができるように、UIの、コードとは独立したところでテストを用意する
2. そのレベルで動作を確認できるようにしながら、内部コードを変更できるようにしていく

現在、このUIレベルのテストは手動/自動関係なく話してます。

# Unit tests for Re-Engineering

> Most developers would agree that unit test should be fully automated,

^ re-engineeringにあるように、現在だと単体テストを書くとか、そこらへんは必要だという認識を多くの人が持っていることと思います。

# Unit tests are not a silver bullet

ですが、さらには以下のようにも描かれています

> but the level of automation for other kind of tests(such as integration tests) is often much lower.

integration layer、UI layerのテストとレベルが高くなってくると自動化を進めることに対してモチベーションがunit testに比べて低くなるようです。

# UI Test should be automated

^ 一方で、

> One area that cries out for automation is UI testing.
> (4.3.2. Regression testing without unit tests)

^ Re-Engineeringにはこのようなことも書かれているように、まさしく、UI Testこそ、自動化する対象として大事な要素になります。

^ しかし、多くの場合はUIテストは多くの時間と人員を使う。なぜなら、モバイルアプリのUIテスト自動化は難しいから。
^ そのため、モバイルアプリのコンテキストでは手動でテスト実行をする傾向にあります。

# Flipped pyramid make development cycle slow

![](images/based_on_test_pyramid_mobile.png)
- http://www.utest.com/articles/mobile-test-pyramid

^ ところで、少し前に私は理想的なテストピラミッドを話しました。
^ unit testが一番大きく、ui testが一番小さいです。
^ ところが、モバイルアプリはこのように理想的なピラミッドとは逆のピラミッドになりやすいです。

^ 手動で動作確認することはテスト自動化よりも楽なためです。
^ ただし、そのままでは実行に時間を多く使う一方になるので将来の俊敏な開発をブロックしてしまいます。

^ そのため、Re-Engineeringを進めるための、特にUIに対するテストを自動化していくことは大事な要素になります。

# UI Test should be automated(again)
^ そのため、UIテストを自動化することはとても大事なのです。

^ 自動で、レイアウトや画面遷移をクラッシュなくできることができます。
^ OSや解像度の組み合わせを人員を集めなくても実施できます。

^ 確かに、ちゃんと設計してテスト自動化を進めることは大事です。
^ そのため、すべての手動テストを汚い自動化されたテストにすべきでもありません。

# implement the strategy

# Automated UI Test with Appium from 2014

^ この問題に対して、私は2014年よりAppiumを中心としたUIテストを強化してきました。
^ 手動テストを実施しながら、徐々に自動化を進めていきました。
^ 言語は表現力や会社の主要言語の関係でRubyをベースにしています。

# Architecture for UI Tests

|シナリオ| <=> ｜操作の実装｜ <=> internal libraries <=> ruby_lib <=> Appium <=> Cookpad App

^ このUIテストの大きなアーキテクチャはこのようになっています。
^ このようにユーザのシナリオと実際のユーザ操作を分けています。
^ ユーザシナリオは実際のiOS環境に関する実装から独立出来ます。
^ iOS環境はユーザシナリオから独立します。
^ こうすることで、ユーザシナリオとiOS側の変更の保守コストを低くしました。

link: http://www.slideshare.net/KazuMatsu/20141018-selenium-appiumcookpad

# Scenarios

```ruby
機能: 複数の条件に合致する検索を正しく行うことができる
  背景:
    前提 'iPhone' で試験を行う

  シナリオアウトライン: ユーザは自分のログイン状態によって変化する検索結果を見ることができる
    * <user_status> ユーザでログインする
    * <search_words> と検索欄から検索する
    * 私は '3' 回下側にスクロールする
    * 画面に 'xxx' が表示されている

    例:
      | user_status | search_words  |
      | 'ps'        | 'ヤシガニ'     |
      | 'non-ps'    | '月食'        |
      | 'guests'    | 'カワエビ'     |
      | 'guest'     | 'テナガエビ'   |
```

^ 基本、シナリオレベルでは自然言語で、普段チームの人たちが使う言葉をベースにそうさを記述します。
^ これは、ユーザを模倣するシナリオを書く時にソースコードレベルの細かなことを書かないようにするためです。
^ そのような細かなものは、unit testなどに任せましょう。
^ シナリオを書く際、人を模倣すると言いましたが例えばspreadsheetなどで管理するようなテストケースをそのままシナリオに落とし込むわけではありません。


# Seasoning
^ 味付け

このUIテストを構築する上で必要な味付けをいくつか共有します

# reduce dependency from internal product code

^ このレベルのUI testで重要なことは、テスト対象となるアプリのViewの構造になるべく依存しないコードを書くことです。
^ 例えば、XPathのような以下のコードはアプリの構造が変化すしたりOSの更新によって頻繁に壊れます。

```
find_element :xpath, //UIAApplication[1]/UIAWindow[1]/UIATableView[1]/UIATableCell[1]
```

そのため、以下のようにaccessibilityIdentifierやaccessibilityLabelを使います

```
find_element :accessibility_id, "an arbitrary identifier"
```

^ ちゃんと分離してテストコードを書くことで、iOSの環境が大きく変化した場合も多くのUIテストを壊すことなく、変化に追従できるようになる。

# Tips2: 環境変数によりテスト対象の挙動を帰る
^ 私たちはiOS Simulatorを主に使います。実機上では実行スピードの関係上、ほとんど使いません。
^ その時、スキーマを変えずとも何らかの挙動を制御したい場合、環境変数を指定します。
^ xcodebuildの話になるのですが、環境変数により挙動を変更することができると、設定によって必要以上にスキーマを増やすことをしなくて済みます

# Tips3: set accessibilityIdentifier with code/storyboard

^ UIAutomationを使っていたころはiOSがXPathによる要素選択をサポートしていました
^ Xcode7からは、Storyboard上でaccessibilityIdentifierを付与することもできるので、iOS8以上をサポートする場合はStoryboard上からViewだけに依存した形で管理、その結果を例えばCSVの一覧として管理すると良いでしょう。差分を追いやすくしておくと、変更に追従しやすくなります。

# tips4: データの境界値は網羅しない

^ なんらかの入力値のバリエーション網羅は、極力unit testに違い側で行うべきです。
^ 無数(a bunch of)の入力パターン全てをUI testで確認することは時間がかかるので避ける必要があります。
^ はじめのうちはui testで用意しても、refactorを続け、unit testが増えていくにつれて削除することは必要です。

# more 🌶️

![](images/go_ahead_image_diff.png)
![](images/go_ahead_request_cap.png)

^ 途中から、このようにimage diffも撮るようになりました。これは結果のジャッジメントを自動化することのほか、デザイナーへのフィードバックとしても利用されます。

# Re-Engineering - re-write / re-factor without fear for developers

^ このような環境を作ることにより、開発者が自信を持って内部コードを書き換え、変更することができるようになります。
^ 複雑な仕組みを書き換えながらも、そのユーザへの影響などはUI Testにより8割、9割はカバーされる状態にしてきました。1年くらいの間はシナリオの調整を中心に行っている感じです。

# introduce Swift

![](images/swift_coverage.png)

^ ここ最近では、機能の追加や変更に加えて私たちのアプリでは、ここ最近Swiftへの置き換えが進んでいます。
^ この書き換えに対しても、このUIに対する自動化されたテストは大いに役立ちます。
^ サービスとして取得している体験を損ねることなく、内部ロジックをSwiftへ書き換えていく。
^ そのようなことを、image diffやnetwork request captureも含めて支援しています。

# faster and more stable

^ モバイルアプリのテスト環境はまだ変化を続けています。
^ XCUITestの登場やEalrGreyといったものも出てきています。
^ FBSimulatorControllerやWebDriverAgentなど。
^ 多くのとても有用なツールが少し前から顔を出し、成長して行っています。
^ Swiftなども変化の波に当面の間のるでしょう。

- 私たちも、より早く安定したautomation testを作りたい

# まとめ

- 自動化されたUI Testsのアーキテクチャと、それらはRe-Engineeringを支えること
- include UI Testsはデザイナも含んだフィードバックサイクルを回す手助けとなる
- 環境の変化の大きなモバイルアプリにおいては、どの程度細かくテストを書き、どの程度テストを書かずにUI Testsに任せるかが大事になる

^ ここまでで、私たちがre-engineeringを行っていくまでに用意したUI Testsの話を味わってみました。
^ また、最近ではそのre-engineeringはデザイナーと行ったチームみんなのへのフィードバックツールへとも役立っていること。

# Thanks

同僚のicons + Thanks

^ 最後に、この会場にも来ている私の同僚の方々にもありがとう
