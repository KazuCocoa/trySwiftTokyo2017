# Tasting tests at Cookpad
@Kazu_cocoa

^ 皆さんこんにちは。クックパッドでテストエンジニアをしています松尾です。SwiftやiOSに関係する人たちの集いで発表することができ、とても緊張しています。
^ 私はテストエンジニアなので、今日の話はテストにまつわるものになります。加えて、私は料理にもかかわる会社に属しているので、tastingとしてみました。

# Who am I?

- Name: Kazuaki Matsuo
- Company: Cookpad .Inc
- Role: Test Engineer / Software Engineer in Quality
- Lang: Swift/ObjC/Java(for Android)/Ruby/Elixir
- maintain: Appium ruby-binding

^ まず自己紹介です。
^ 私は普段はモバイルアプリのテスト自動化やプロセス改善、もっと大きく組織的な改善活動にも関わっています。テストだけではないので、Software Engineer in Qualityと呼べるような働き方かもしれません。
^ 開発言語としてはSwiftなどの他にはRuby/Elixir/Java for Androidに触れることが多いです。
^ 少し前から、AppiumのRuby bindingをメンテナンスしています。モバイルアプリ開発者の中には、ライブラリを使ってくれた方がいるかもしれません。

# 何を味わうか?

![](images/Test-Pyramid-Adventures-in-QA.png)

^ 一言でテスト、といっても、いくつか種類があります。
^ このように、開発時によくかくロジックのテストであるUnit testから、UIを操作してユーザの操作を模倣するようなテストまであります。

# どれだけUI Testが私たちの開発を支えたか
^ 今日はこの中でUI Testが何を支えるか、を味わってみます。

# テストの話はテスト対象をのけ者にはできない

^ テストの話をする時、そのテスト対象となる製品の話をのけ者にすることはできません。
^ そのため、少しCookpadについて話し、テスト対象となるiOSアプリへと話を移していきます。

# What is Cookpad?

^ Cookpadはレシピ共有サービスを提供しています。

# Cookpad for the world
https://www.similarweb.com/top-websites/category/food-and-drink/cooking-and-recipes

^ 最近では海外でもシェアを広げ、simularweb.comではfoodカテゴリで最大のものとなっています。

# Cookpad for iOS(Japan and Global)
日本のスクショと、海外向けのスクショを載せる

^ クックパッドの主なiOSアプリには2種類あります。それは日本向けのアプリと、海外向けのアプリです。
^ 国外からいらっしゃった方は、この海外向けのものをよく見るとおもいます。
^ 今日は、この日本向けのアプリがテスト対象です。

# History for Cookpad iOS App

- クックパッドアプリの遷移

^ このクックパッドアプリはすでに5年の時を経ています。その間、UIを複数回大きく変えました。
^ 2013年に大きくアプリを作り変え、2014年にUIをiOS6の頃から変更し、2015年にはiOS8?7?向けに変更し...
^ このように、見た目も変えながら、中身も最近ではSwiftへと置き換えを進めています。
^ ソースコードも順調に増え、今では10万行ものコードが存在します。

# Quality in Japan

kano-modelを表示する

^ ところで、比較的見やすい品質モデルにkano-modelがあります。このモデルには当たり前品質を魅力的品質の2種類があります。
^ 日本では、この当たり前品質の要求が高く、特に基本的な機能が動作すること、例えば画面遷移ではクラッシュしないことなどの要求が高いです。

# Quality in Mobile

Diachronic Quality

^ diachronic qualityという造語があります。
^ これは、変わり続ける品質を説明するものです。言語学から影響を受けています。
^ モバイルアプリは変化が大きなアプリなので、この変化し続ける世界においても、先ほど挙げた日本のユーザが当たり前だと感じる明らかな不具合を減らす必要があります。

# Change, Change, Change...
- 2week ~ 1month release sycle
- Change UI / Code many times since Apple require us change

^ 私たちのアプリは、2週間〜1か月のスパンでここ2年間リリースを続けています。
^ その間、この作り始めたUIテストは画像diffによる不具合検出など機能を増やしています。

# ビジネスへの挑戦 - Re-Engineering

サービスはビジネスへの挑戦の為に、試行錯誤します。

# Re-Write/Re-Factor - Re-Engineering

> unit testが大事であることは、疑いようはない
> Unit tests are not a silver bullet.

^ 高頻度の変更のある開発において、Swiftだとtypeをしっかり使うことやunit testやそのCI環境が基軸となることは最近では多くの人が納得することでしょう。
^ ただ、5年とか前のアプリにおいて、十分にテストコードが書かれたものは少ないのではないでしょうか。

# UI Test to support Re-Engineering

> One area that cries out for automation is UI testing.
> (4.3.2. Regression testing without unit tests)

- Re-Engineeringという本に書いていたのですが、まさしくUI Testこそ、変化に追従し、変化に追従するに当たって大事な要素になります。
^ UIやシナリオの設計(体験の設計)が差別的な競争力になるモバイルアプリではなお。
^ iOSでは、最近のSwiftへの置き換えも進めるように、UIレベル、つまりユーザが目にする範囲において確実に動作することが確認出来る環境を持っていることは大きな優位性になります。
^ 社内で働くiOSエンジニアの多くも、自分の実装によって自分の想定していない不具合も表示されるものは特に、検出される可能性が高いことは心理的安全性にもつながります。
^ 実装の書き換えに怯えなくて良くなりますね。

# Automated UI Test with Appium from 2014

^ この問題に対して、私は2014年よりAppiumを中心としたUIテストを強化してきました。言語は表現力や会社の主要言語の関係でRubyをベースにしています。
^ マニュアルテストだけのテスト要員はおらず、基本的にはこのUIテストによる多くのiOSのバリエーションに対するテストでテストを続けきました。
^ 自動化されたテストは、多くの場合は3回以上実行すると元が取れるといわれます。(要出典)

# Re-Engineering - jump up to Swift

^ 私たちのアプリでは、ここ先んSwiftへの置き換えが進んでいます。

# feedback to designers to catch up with UI

^ また、このようなimagediffはデザイナーへのフィードバックにもなります。
^ 自分の修正が期待通りか、前回と比べてどの程度違和感がないかなど。

# wrap up

^ どこに大きく変化が訪れ、それに対してどのように対策していくか。
^ 私たちの場合は、長く続くサービス、変化を続けるアプリや内部コードに対して、UIテストがもたらす恩恵をお話ししました。

# Tips

^ ここまでコードの話をしませんでしたが、tipsを少し。
^ 皆さんもお使いかもしれませんが、表示の変化に追従するためにaccessibilityIdentifierをうまく使いましょう。
^ Xcode8からはStoryboardにおいても簡単に設定できるようになりました。
^ コードへの知見がなくとも、Storybardを触ることができるのであれば用意にidを付与できます。
^ Viewが置き換わらない限り、座標の変更程度であればaccessibilityIdentifierを中心に記述されたUIテストは壊れることはあまりありません。

# これから

^ モバイルアプリのテスト環境はまだ変化を続けています。
^ XCUITestの登場やEalrGreyの登場。
^ FBSimulatorControllerやWebDriverAgentなど。
^ 多くのとても有用なツールが少し前から顔を出し、成長して行っています。
^ Swiftなども変化の波に当面の間のるでしょう。
^ その間も、

# Thanks

同僚のicons + Thanks

^ 最後に、この会場にも来ている私の同僚の方々にもありがとう

