# Tasting tests at Cookpad
@Kazu_cocoa

^ 皆さんこんにちは。クックパッドでテストエンジニアをしています松尾です。SwiftやiOSに関係する人たちの集いで発表することができ、とても緊張しています。
^ 私はテストエンジニアなので、今日の話はテストにまつわるものになります。私は料理にもかかわる会社に属しているので、タイトルはtastingとしてみました。

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

# Tests?
^ 一言でテスト、といっても、いくつか種類があります。
^ Usually, "test" include a bunch of types.

^ 例えば、usability testやperformanceテストといったカテゴリの話があったり、unit test/integration testといったテストレベルの話であったり。
^ 今日は、テストピラミッドと呼ばれるunit testやintegration test、UI testと区分される話に焦点を当てて話をします。

# Based on test pyramid

![](images/based_on_test_pyramid.png)

- http://www.utest.com/articles/mobile-test-pyramid

^ このピラミッドは目にすることが多いかもしれません。
^ 実施するテストレベルと、その量がどのような関係にあると理想的か、ということを表した図です。
^ いわゆるメソッド単位でのロジックの確認を中心とするunit testから、Viewを操作する、ユーザの操作を模倣するようなUI Testまで存在しています。

# How UI Tests support our product
^ どれだけUI Testが私たちの開発を支えたか

^ 今日はこの中でUI Testが何を支えるか、をtastingしてみようと思います。
^ これの結果、UI Testの価値やそこへの取り組みのモチベーションにつながれば嬉しいです。

# テストの話はテスト対象をのけ者にはできない

^ ところで、ツール以上のテストの話をする時、そのテスト対象となる製品の話をのけ者にすることはできません。
^ そのため、少しCookpadについて話し、今回テスト対象となるiOSアプリがどんなものかを味わっていきます。

# What is Cookpad?

![](images/about_cookpad_en.png)
![](images/about_cookpad_jp.png)

^ Cookpadはレシピ共有サービスを提供しています。始まりはWebサービスからでした。
^ 現在は日本向けのものと、日本以外に向けたものを提供しています。これは、Webサービスの成熟度の違いからきていますが、いずれも同じcookpadです。

# Cookpad for the world
https://www.similarweb.com/top-websites/category/food-and-drink/cooking-and-recipes

^ 最近では海外でもシェアを広げ、simularweb.comではfoodカテゴリで最大のものとなっています。

# Cookpad for iOS(Japan and Global)

![](images/cookpad_for_ios_japan.png)
![](images/cookpad_for_ios_global.png)

^ クックパッドの主なiOSアプリには2種類あります。それは日本向けのアプリと、日本以外に向けたアプリです。
^ 国外からいらっしゃった方は、この海外向けのものをよく見るとおもいます。
^ 今日は、この日本向けのアプリを対象に話します。

# History for Cookpad iOS App

![](images/history_for_cookpad_ios_image1.png)
![](images/history_for_cookpad_ios_image2.png)
![](images/history_for_cookpad_ios_image3.png)
![](images/history_for_cookpad_ios_image4.png)
![](images/history_for_cookpad_ios_graph.png)

^ このクックパッドアプリはすでに5年の時を経ています。その間、UIを複数回大きく変えました。
^ 2013年に大きくアプリを作り変え、2014年にUIをiOS6の頃から変更し、2015年にはiOS8?7?向けに変更しました。
^ このように、見た目も変えながら、最近では中身も最近ではSwiftへと置き換えを進めています。<= もしかしたら、最近のSwiftのコードの%を載せるかも
^ ソースコードも順調に増え、今では10万行ものコードが存在します。

# History for UI Tests against Cookpad iOS App

![](images/history_for_ui_tests.png)

^ 2014年の頃からUI Tests、特にAppiumを使った環境を作っていきました
^ 現在、すでに2017年になりますが、その当時からのツールを今も発展させながら使い続けています
^ この間、先ほど見せたようにUIを変化させながらも、このテストコードの拡充とマニュアルテストによって変化を支えてきました。

# Quality in Japan

- 日本列島の画像

^ 今回のiOSアプリが対象とする国は主には日本です。そこで、日本のアプリに対する見方を少し共有します。

# kano-model based quality

![](images/kano_model_based_quality.png)

https://en.wikipedia.org/wiki/Kano_model

^ 比較的見やすい品質モデルにkano-modelがあります。このモデルには当たり前品質を魅力的品質の2種類があります。
^ 日本では、この当たり前品質の要求として特に基本的な機能が動作すること、例えば画面遷移ではクラッシュしないことなどの要求が高いです。
^ そのため、そういうことが当たり前と感じる人が多い傾向にあるようです。(cookpadのレビューと不具合を参考にすると)

- 何か参考資料持ってこれたらな...

# Quality in Mobile App

Diachronic Quality

^ diachronic qualityという造語があります。
^ これは、変わり続ける品質を説明しようとしていることばです。言語学から影響を受けています。
^ モバイルアプリ、特にサービスとして提供しているアプリは時代の流れに合わせて変化が大きくなるので、この変化し続ける世界においても、先ほど挙げた日本のユーザが当たり前だと感じる明らかな不具合を減らす必要があります。

メモ: ここは除いた方が良いかもしれない

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

- Cookpadアプリの変化の遷移
- 日本における、アプリの動作で基本的なものとして求められること
- モバイルアプリは特に、変化し続けることが求められる環境にある

^ 10分くらいにしておきたい

# Tasting tests :yummy:

# Re-Engineeringに足を踏み込むとき

何か良い画像を埋め込みたい

^ クックパッドアプリは、今ではシェアを多く持っていますが、以前は試行錯誤が中心でした。
^ そこから、UIを整えたり、機能を整えたり、開発人数が増えた上でもそれを維持する仕組みが必要になってきました。
^ そのため、re-writeやrefactorを推し進め、継続して開発を続ける体制を作る必要がありました
^ そう、re-engineeringを進める段階になっていました <= 微妙かも...

# jump into Re-Engineering

> Writing unit tests before refactoring is sometimes impossible and often pointless.

^ rewriteやリファクタを推し進める時、高頻度でテストが行われ、それを元に正しいことを確認し続ける環境を持つことは最近では必要だと知っている人が多いで賞。

# Strategy for Re-Engineering

# unit tests for Re-Engineering

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

# Mobile app tend to be flipped pyramid easily

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
^ Webアプリに触れたことがある人はわかるかもしれませんが、Cucmberを使う時の構造に似ていますね。また、責務の分離はエンジニアに取っても馴染みの深いものかと思います。

link: http://www.slideshare.net/KazuMatsu/20141018-selenium-appiumcookpad

# Test Scenarios

^ 日本語ですが、

# Go ahead

- Image Diff / network diff

^ 途中から、このようにimage diffも撮るようになりました。これは結果のジャッジメントを自動化することのほか、デザイナーへのフィードバックとしても利用されます。

# Re-Engineering - re-write / re-factor without fear for developers

^ このような環境を作ることにより、開発者が自信を持って内部コードを書き換え、変更することができるようになります。
^ 複雑な仕組みを書き換えながらも、そのユーザへの影響などはUI Testにより8割、9割はカバーされる状態になります。

# Swiftを入れていく

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
