# Tasting tests at Cookpad
`@Kazu_cocoa`

^ 皆さんこんにちは。クックパッドでテストエンジニアをしています松尾です。今日はSwiftやiOSに関係する人たちの集いで発表することができ、とても緊張しています。
^ 私はテストエンジニアなので、今日の話はテストにまつわるものになります。Swift自体の話も少なめです。
^ ちなみに、このタイトルは私は料理にもかかわる会社に属しているのでtastingとしてみました。

# About me

- Name: Kazuaki Matsuo
- Company: Cookpad .Inc
- Role: Test Engineer / Software Engineer in Quality
- Dev: :swift: / :ruby: / :java: for  :android: / :elixir: :erlang:
- maintain: Appium ruby-binding

![](images/about_me_appium.png)

^ まず自己紹介です。
^ 私は普段はモバイルアプリのテスト自動化やプロセス改善、もっと大きく組織的な改善活動にも関わっています。
^ 普段の活動はテストだけではないので、Software Engineer in Qualityと呼べるような品質に対していろいろな取り組みを行う、幅広い働き方かもしれません。
^ 開発言語としてはSwiftなどの他にはRuby/Elixir/Java for Androidに触れることが多いです。
^ 少し前から、AppiumのRuby bindingをメンテナンスしています。Appiumはモバイルアプリ向けのツールなので、もしかしたらこの会場に来ている人の中にはライブラリを使ってくれた方がいるかもしれません。

# 😋

# A bunch of themes in tests
^ 一言でテスト、といっても、様々なテーマがあります。
^ Usually, "test" include a bunch of types.

^ 例えば、usability testやperformanceテストといったカテゴリの話があったり、unit test/integration testといったテストレベルの話であったり。
^ それらの中で、今日はテストピラミッドと呼ばれるunit testやintegration test、UI testと区分されるテーマに関してお話をします。

# test pyramid

![](images/based_on_test_pyramid.png)

- http://www.utest.com/articles/mobile-test-pyramid

^ このピラミッドを目にしたことがある人は多いかもしれません。
^ 実施するunit test/integration test/ui testの量がどのような関係にあると理想的か、ということを表した図です。
^ 多くの場合、unit testはメソッド単位のテスト、UI testがユーザの操作を模倣するような粒度での話になります。

# How UI Tests support our product
^ どれだけUI Testが私たちの開発を支えたか

^ 今日はこの中でUI Testが私たちの何を支えたのか、をtastingしてみようと思います。
^ これの結果、UI Testの価値やそこへの取り組みのモチベーションにつながれば嬉しいです。
^ Siwftによるunit testレベルの話は他の発表があるようなのでそちらを楽しみにしてください。

# テストの話はテスト対象をのけ者にはできない 🙅

^ ツール以上のテストの話をする時、そのテスト対象となる製品の話をのけ者にすることはできません。
^ そのため、少し私の属しているCookpadについて話し、今回テスト対象となるiOSアプリがどんなものかを味わってみます。

# What is Cookpad?

![](images/what_is_cookpad_world.png)

https://www.similarweb.com/top-websites/category/food-and-drink/cooking-and-recipes

^ Cookpadはレシピ共有サービスを提供しています。始まりはWebサービスからでした。
^ 現在は日本向けのものと、日本以外に向けたものを提供しています。これは、Webサービスの成熟度の違いからきていますが、いずれも同じcookpadです。
^ 最近では海外でもシェアを広げ、simularweb.comではfoodカテゴリで最大のものとなっています。
^ アプリはiOS/Androidともに出しています。

# Cookpad for iOS(Japan and Global)

![](images/cookpad_for_ios_japan.png)
![](images/cookpad_for_ios_global.png)

^ クックパッドの主なiOSアプリには2種類あります。それは日本向けのアプリと、日本以外に向けたアプリです。
^ 国外からいらっしゃった方は、この海外向けのものをよく見るとおもいます。
^ 今日は、この日本向けのアプリを対象に話します。

# Cookpad for iOS(Global)

![](images/cookpad_for_ios_global.png)

^ 国外からいらっしゃった方は、この海外向けのものをよく見るかもしれません。

# Cookpad for iOS(Japan)

![](images/cookpad_for_ios_japan.png)

^ ただ、今日は、この日本向けのアプリを対象に話します。

# History for Cookpad iOS App

![](images/history_for_cookpad_ios_image1.png)
![](images/history_for_cookpad_ios_image2.png)
![](images/history_for_cookpad_ios_image3.png)
![](images/history_for_cookpad_ios_image4.png)
![](images/history_for_cookpad_ios_graph.png)

^ このクックパッドアプリはすでに5年の時を経ています。その間、UIを複数回大きく変えました。
^ 2013年に大きくアプリを作り変え、2014年にUIをiOS6の頃から変更し、2015、16年と機能をいろいろ追加したり、除いたりしながら試行錯誤してきました。
^ 見た目も変えるのですが、例えば中身もSwiftへと置き換えを進めているように多くのre-write/refactorをコードレベルでも加えています。
^ ソースコードも順調に増え、今では10万行ものコードが存在します。

# Quality in Japan market

![](images/quality_in_japan_.png)

^ テスト対象となるアプリが長年にわたり変化してきたことを共有しました。
^ 次に、私たちの主なサービスの対象としていた日本市場の特徴をみてみます。
^ 少し、日本のアプリに対する見方を少し共有します。

# kano-model based quality

![](images/kano_model_based_quality.png)

https://en.wikipedia.org/wiki/Kano_model

^ 比較的見やすい品質モデルにkano-modelがあります。このモデルには当たり前品質を魅力的品質の2種類があります。
^ 日本では、この当たり前品質の要求として特に基本的な機能が動作すること、例えば画面遷移ではクラッシュしないことなどの要求が高いです。
^ そのため、そういうことが当たり前と感じる人が多い傾向にあるようです。(cookpadのレビューと不具合を参考にすると)

# Diachronic Quality in Mobile App

^ diachronic qualityという造語があります。
^ これは、変わり続ける品質を説明しようとしていることばです。言語学から影響を受けています。
^ モバイルアプリ、特にサービスとして提供しているアプリは時代の流れに合わせて変化が大きくなるので、この変化し続ける世界においても、先ほど挙げた日本のユーザが当たり前だと感じる明らかな不具合を減らす必要があります。

# Change, Change, Change...

- environment
  - iOS5 => iOS6 => iOS7 => iOS8 => iOS9 => iOS10...
    - include changeing GUIs
  - Objective-C => Swift

^ iOS周りの変化を説明
^ iOS6, 7, 8...
^ Objective-C, Swift!!
^ プラットフォームの変化に合わせて、時代によって求められるQualtyも変化していってます

# Changes in Cookpad

- サービス拡大のための挑戦
    - Change UIs, features...
- 2week ~ 1month release cycle
- Change UI / Code many times since Apple require us change

^ この間、この時代に沿ったり、Cookpad独自に変化しようとするように、cookpadにおける"変化"を詳しく見てみると、このように細かく、頻繁に変化しています
^ その間、私たちのアプリは、2週間〜1か月のスパンでここ2年間リリースを続けています。
^ 最近では、1回のリリースには5,000~10,000行程度の変更が加わりながらリリースされています。

# ここまでで話したこと

- Cookpadアプリの変化の歴史
- 日本市場が求めるもの
- モバイルアプリをとりまく変化し続ける品質

^ 10分くらいにしておきたい

# Tasting tests😋

^ では、この環境の中で行ってきたUI Testの話をしていきたいと思います。

# History for UI Tests against Cookpad iOS App

![](images/history_for_ui_tests.png)

^ このgithubリポジトリは、automated ui testのツール群の成長の軌跡です。
^ 2014年の頃からUI Tests、特にAppiumを使った環境を作っていきました。
^ 現在、すでに2017年になりますが、その当時からのツールを今も発展させながら使い続けています。
^ この間、先ほどのiOSアプリの変化の歴史をこの自動化されたテストによって支えてきました。

# ここまでUI Testになぜ力を入れていたか🤔

# Re-Engineering

何か良い画像を埋め込みたい

^ クックパッドアプリは、今ではシェアを多く持っていますが、以前は試行錯誤が中心でした。
^ そこから、UIを整えたり、機能を整えたり、開発人数が増えた上でもそれを維持する仕組みが必要になってきました。
^ そのため、re-writeやrefactorを推し進め、継続して開発を続ける体制を作る必要がありました

# Basic strategy for Re-Engineering

> Writing unit tests before refactoring is sometimes impossible and often pointless.

^ rewriteやリファクタを推し進める時、高頻度でテストが行われ、それを元に正しいことを確認し続ける環境を持つことは最近では必要だと知っている人が多いでしょう

# Unit tests for Re-Engineering

> Most developers would agree that unit test should be fully automated,

^ 最近出たre-engineeringにあるように、現在だと単体テストを書くとか、そこらへんは必要だという認識を多くの人が持っていることと思います。
^ また、Swiftだとtypeをしっかり使うことやunit testやそのCI環境が基軸となることは最近では多くの人が納得することでしょう。
^ ただ、5年とか前のアプリにおいて、十分にテストコードが書かれたものは少ないのではないでしょうか。

# Unit tests are not a silver bullet

> but the level of automation for other kind of tests(such as integration tests) is often much lower.

# UI Test to support Re-Engineering

> One area that cries out for automation is UI testing.
> (4.3.2. Regression testing without unit tests)

^ Re-Engineeringにはこのようなことも書かれているように、まさしく、UI Testこそ、変化に追従し、変化に追従するに当たって大事な要素になります。
^ UIやシナリオの設計(体験の設計)が差別的な競争力になるモバイルアプリではなお。
^ iOSでは、最近のSwiftへの置き換えも進めるように、UIレベル、つまりユーザが目にする範囲において確実に動作することが確認出来る環境を持っていることは大きな優位性になります。
^ 社内で働くiOSエンジニアの多くも、自分の実装によって自分の想定していない不具合も表示されるものは特に、検出される可能性が高いことは心理的安全性にもつながります。
^ 実装の書き換えに怯えなくて良くなりますね。

# Test environment for Mobile app tend to be flipped pyramid easily

![](images/based_on_test_pyramid_mobile.png)
- http://www.utest.com/articles/mobile-test-pyramid

^ モバイルアプリはこのように理想的なピラミッドとは逆のピラミッドになりやすい
^ そのため、automated ui testの、特にViewに対するものまでちゃんとよういすることが短時間で最低限のチェックを回すには必要になる。

# Automated UI Test with Appium from 2014

^ この問題に対して、私は2014年よりAppiumを中心としたUIテストを強化してきました。言語は表現力や会社の主要言語の関係でRubyをベースにしています。
^ マニュアルテストだけのテスト要員はおらず、基本的にはこのUIテストによる多くのiOSのバリエーションに対するテストでテストを続けきました。
^ 自動化されたテストは、多くの場合は3回以上実行すると元が取れるといわれます。(要出典)

# Architecture for UI Tests

|シナリオ| <=> ｜操作の実装｜ <=> internal libraries <=> ruby_lib <=> Appium <=> Cookpad App

^ このUIテストの大きなアーキテクチャはこのようになっています。
^ このおおまかな形は2014年から変わることなく続いています。
^ これは、クックパッドアプリとしての独自ドメインであるシナリオと、AppiumやiOSの環境といった実際の環境を分離している状態です。
^ Webアプリに触れたことがある人はわかるかもしれませんが、Cucumberを使う時の構造に似ていますね。また、責務の分離はエンジニアに取っても馴染みの深いものかと思います。

link: http://www.slideshare.net/KazuMatsu/20141018-selenium-appiumcookpad

# Scenarios

```ruby
例を載せる
```

^ 基本、シナリオレベルでは自然言語で、普段チームの人たちが使う言葉をベースにそうさを記述します。
^ これは、ユーザを模倣するシナリオを書く時にソースコードレベルの細かなことを書かないようにするためです。
^ そのような細かなものは、unit testなどに任せましょう。

# what kind of scenarios do we describe
^ シナリオを書く際、人を模倣すると言いましたが例えばspreadsheetなどで管理するようなテストケースをそのままシナリオに落とし込むわけではありません。
^ iOSアプリのテストでは、simulaltorの初期化や起動などに時間が必要なので、ある程度のシナリオをまとめて実行するようにしたりします。
^ また、人が繰り返しやるには大変な長いシナリオを実施させたりもします。
^ 例えばクライアントのキャッシュを超えた時間を待った後、ちゃんとViewが再描画されるか、というものも確認することがあります。

# 環境変数によりテスト対象の挙動を帰る
^ 私たちはiOS Simulatorを主に使います。実機上では実行スピードの関係上、ほとんど使いません。
^ その時、スキーマを変えずとも何らかの挙動を制御したい場合、環境変数を指定します。
^ xcodebuildの話になるのですが、

# Tips(時間があまりそうだったら書く)

- find elements with accessibilityIdentifier

^ UIAutomationを使っていたころはiOSがXPathによる要素選択をサポートしていました
^ ただ、現在のXCUITestはそうではないため、

# Go ahead

- Image Diff / network diff

^ 途中から、このようにimage diffも撮るようになりました。これは結果のジャッジメントを自動化することのほか、デザイナーへのフィードバックとしても利用されます。

# Re-Engineering - re-write / re-factor without fear for developers

^ このような環境を作ることにより、開発者が自信を持って内部コードを書き換え、変更することができるようになります。
^ 複雑な仕組みを書き換えながらも、そのユーザへの影響などはUI Testにより8割、9割はカバーされる状態になります。

# introduce Swift

![](images/swift_coverage.png)

^ ここ最近では、機能の追加や変更に加えて私たちのアプリでは、ここ最近Swiftへの置き換えが進んでいます。
^ この書き換えに対しても、このUIに対する自動化されたテストは大いに役立ちます。
^ サービスとして取得している体験を損ねることなく、内部ロジックをSwiftへ書き換えていく。
^ そのようなことを、image diffやnetwork request captureも含めて支援しています。

# More faster and stable

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
