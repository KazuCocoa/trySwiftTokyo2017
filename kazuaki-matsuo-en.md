# Tasting tests at Cookpad
@Kazu_cocoa

Hello, everyone.
I'm Kazu.
Now, I'm so happy and excited to be able to talk for many Swift and iOS developers.

Today's my topic is associated with "TEST" since I'm a test engineer at Cookpad.
"Tasting" used in my title means taste food stuff because my company is regarding with food.

# About me

First, I introduce myself.
I'm Kazuaki Matsuo and working at Cookpad as a test engineer.
I've tried test automation for Android and iOS and improved development processes and other many roles to improve several qualities.
So, "Software Engineer in Quality" might be more suitable name than test engineer to explain me in my company, I think.

I use some languages in my work such as swift, ruby, java for android and elixir.
Recently, I've maintained ruby binding client library for Appium.

# 😋
go ahead

# A bunch of topics in "TEST"
Even we use the word "TEST", it has various topics.

For example, the word has categories such as usability test and performance test and has test level such as unit test and integration test.
Today, I pick up a test pyramid which has three layers, unit test, integration test and UI test for automated test. In addition the pyramid has manual test outside of the pyramid.

# test pyramid

![](images/based_on_test_pyramid.png)

The pyramid is one of a famous diagram for test automation.
This show ideal relationship and amount for unit tests, integration tests and UI tests in development.
Unit tests deal with testing logic in code level and UI tests focus on simulate user behaviours against test target app.
Unit tests are small and fast but UI tests aren't.

# How UI Tests support our development
Today, you can taste UI tests and our story.
I'm happy if anyone gets the motivation to try UI tests after my talk.
Meanwhile, I don't talk about unit level tests such as mock, protocol oriented..

# We should know about the test target if we try to tests stuff
(いまいち...)

We should learn test target if we try to understand and taste some tests not only about tools but also strategies.
So, I'll explain about Cookpad and its iOS app at first to help you understand the following topics.

# What is Cookpad?

![](images/what_is_cookpad_world.png)

Cookpad is one of famous recipe sharing service in the world.
We have two kinds of the service, for Japan and for rest of the world for now.
According to the similarweb.com, Cookpad is the largest site in the food category.

# Cookpad for iOS(Japan and Global)

![](images/cookpad_for_ios_japan.png)
![](images/cookpad_for_ios_global.png)

We also have two kinds of iOS applications for Cookpad.
One is for Japan and another is for rest of the world.
They are difference service growth level, so we haven't merged them yet.

If anyone comes from out of Japan, you can see global app.

# Cookpad for iOS(Japan)

![](images/cookpad_for_ios_global.png)

I focus on the Japanese app today.

# History for Cookpad iOS App

![](images/history_for_cookpad_ios_image1.png)
![](images/history_for_cookpad_ios_image2.png)
![](images/history_for_cookpad_ios_image3.png)
![](images/history_for_cookpad_ios_image4.png)
![](images/history_for_cookpad_ios_graph.png)

The cookpad app has grown for around 5 years.
I attached some screenshots to be able to check the growth and the changes.
The app changed UI component, add or delete any features or re-write/refactor implementations during the period.

The production code also has grown and it is around 100 thousand lines except for comment, blank and new lines for now.

# Kano-model and Japan market

![](images/kano_model_based_quality.png)

https://en.wikipedia.org/wiki/Kano_model

kano-model is one of the famous models to explain about quality.
There is two main quality. One is Must-be Quality and another is Attractive Quality.
Must-be quality in Japan is high because they require crash-free app as must-be quality in many cases. It is not attractive for them.

# diachronic quality in mobile app

Mobile app's environment changes frequently and OS version change every year.
UI and design also change a few years cycle.
Required quality by market also has changed.

Recently, I sometimes address as diachronic quality like this movement.
This name comes from linguistics.

# Changes in Cookpad

- release cycle: 2week ~ 1months
- change ui / code

In this period, Cookpad also has changed to catch up with the cycle.
Release our app every two weeks or one month to challenge our service and UIs for the end users.
Recently, we change source code around 5,000 ~ 10,000 lines per release.

# summary

Histories of Cookpad iOS app and its changes.
diachronic quality in mobile.

# Tasting tests😋

I start talking UI Test what I've done for the environment.

# History for UI Tests for Cookpad iOS App

![](images/history_for_ui_tests.png)

This repository shows a growth of UI tests I implemented at Cookpad.
I've developed the environment since 2014.
I've supported the changes with this kinds of UI tests.

# Why have we implemented this UI tests?

# Re-Engineering

Start tasting tests to re-engineering.
Especially, I talk about how to step into re-write/refactor code.

# Should we taste from?

> Writing unit tests before refactoring is sometimes impossible and often pointless.

According to the re-engineering, the quotation is described.
it is true since we can't check behaviour without tests.
The most of the developers may agree with re-write/refactor features without tests lead unexpected broken stuff.
BTW, to make the target app testable, we should consider architecture for the app and other many things.

On the other hand, without CI environment, it is difficult to iterate development cycle quickly without tests.

-----ここまで-----

# Basic strategy for Re-Engineering

  (internal) sorce code => |app| <= (externl) users

In this case, we approached to make the app testable from two aspects, internal and external.
"Internal" means product source code side.
"External" means end-user and GUI side.

# Make checkable from external to internal

check from external <=> re-write/refactor/implement from internal(and add unit tests)
図を用意する

Check if GUI/behaviour are broken from external.
And re-write/refactor/implement some features.
Developers continue to change code aggressive because if some feature was broken, we can uncover the bug in UI level.
So, we can fix the issue before release.

# Unit tests for Re-Engineering

The re-engineering also describes the following quotation.

> Most developers would agree that unit test should be fully automated,

I and most of the developers agree with this, I think.

# Unit tests are not a silver bullet

But, it also describes as...

> but the level of automation for other kind of tests(such as integration tests) is often much lower.

# UI Test to support Re-Engineering

But....

> One area that cries out for automation is UI testing.
> (4.3.2. Regression testing without unit tests)

So, UI tests take too many time and too many human resources in mobile in many cases.
Because test automation for mobile is difficult than we app.

But, automated UI tests can support re-engineering in many times.
You can check automatically most of the layouts, screen transactions without crashes and so on.
You can also check combinations of various OS versions and resolutions without additional human resources.

This benefit also lead psychological safety for developers.

# Flipped pyramid make development cycle slow

![](images/based_on_test_pyramid_mobile.png)

I talked ideal test pyramid for test automation before.
But in the mobile context, it is easy to make it flipped.
Because checking UIs manually is easy than test automation but it blocks swift development cycle in the future.

# implement the strategy

# Automated UI Test with Appium from 2014

So, I've tried to implement UI Test since 2014, I've joined cookpad.
While conducting manual tests, I've been working on test automation step by step.
I've implemented it with Ruby :p

# Architecture for UI Tests

図にする
|シナリオ| <=> ｜操作の実装｜ <=> internal libraries <=> ruby_lib(appium ruby binding) <=> Appium <=> iOS(UIAutomation/XCUITest) <=> Cookpad App

Our architecture for the automated test is like this.
We separate some layer to divide responsibilities for scenarios associated with end-users and product code associated with the iOS framework.

I'd like to independent scenarios from the iOS side and also independent implementations from user scenarios.
(iOS側の実装と、シナリオ側の実装を分離したい)

(こうすることで、iOS側が変化した時は、シナリオは変えず、internal librariesのところだけでiOSフレームワーク側の変更を吸収します)

Thus, we can decrease maintenance costs for scenarios side and iOS side.

The separation of responsibility is familiar to developers.


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

This is an example to describe scenarios.
I implement scenarios with data-driven testing with Turnip.
Turnip is similar to Cucumber.
This scenario is close to end-user. So, I chose the national language to describe the scenarios.
This scenario is not equal to test case which conducted by manual.

# Seasoning

# Tips1: reduce dependency with production code
It is important to describe test scenarios independent of internal logic for production code.
For example, the following finding elements on view with XPath will be broken easily if update OS version from iOS7 to iOS8. Because the path strongly depends on the iOS side.

```
find_element :xpath, //UIAApplication[1]/UIAWindow[1]/UIATableView[1]/UIATableCell[1]
```

So, it is better to implement with accessibilityIdentifier or accessibilityLabel than xpath.

```
find_element :accessibility_id, "arbitrary identifier"
```

Keep independent with scenarios and internal logic for production is also important for this kind of tests.

# tips2: Don't run tests for all boundaries
Test for all boundaries is better to implement in the unit test.
Because UI test is too slower than the unit test.
So, if you implement all boundaries in UI side, it is better to move test from UI to unit and remove it from UI tests in the future.

# more 🌶️

We also implement image diff to judge the results and feedback to designers.
Designers can know the differences between the previous version and new version easily. This helps their checking.

And we also capture network traffic because we'd like to check logging requests.
Because the requests are very important for service development to collect data.

# Re-Engineering - re-write / re-factor without fear for developers
Keeping this kind of UI tests encourage developers re-write and refactor source code and introduce new tests in unit level.
If their changes broke some features, UI tests can uncover the errors because our tests cover around 80~90% screen transactions for now.

# introduce Swift
We start to introducing Swift a few months ago.
Also in this case, UI tests help fearless changes for developers in UI level.

# faster and more stable
Current UI tests are enough for current our development process for now.
But our team will become bigger than now in the future.
So, I'll introduce alternative tools such as XCUITest or EarlGrey for UI tests partially. But we don't stop using Appium because their responsibility area is different.

# Conclusion
I talked about histories of cookpad app and how we've tried to re-engineering the big app with UI tests.
UI tests need to separate responsibility from production code to catch up with some changes painless.

# Thanks
Thanks for listening my talk.
And our co-workers.
今日の話は、チーム全体として動かないとうまくいかないものだった。

