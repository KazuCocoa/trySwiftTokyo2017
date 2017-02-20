# Tasting tests at Cookpad
@Kazu_cocoa

Hello everyone.
I'm Kazu.
Now, I'm so happy and exciting to be able to talk for many Swift and iOS develpers.

Today's my topic is associated with "TEST" since I'm test engineer at Cookpad.
"Tasting" used in my title means taste food stuff because my company is regarding with food.

# About me

First, I introduce myself.
I'm kazuaki matsuo and working at Cookpad as test engineer.
I've tried test automation for Android and iOS, and improved development processes and other many role to imprpve quality.
So, "Software Engineer in Quality" might be more suitable name than test engineer in my company, I think.

I use some languages in my work such as swift, ruby, java for android and elixir.
Recently, I've maintained ruby binding client library for Appium.

# 😋
go ahead

# A bunch of topics in "TEST"
Even we use the word "TEST", it has various topics.

For example, the word has categories such as usability test and performance test, and has test level such as unit test and integration test.
Today, I pick up a test pyramid which has three layers, unit test, integration test and ui test for automated test and manual test.

# test pyramid
This pyramid is one of famous figure for test automation.
The pyramid means ideal relationship and amount between unit tests, integration tests and UI tests in development.
Unit tests deal with testing logic in code level and ui tests focus on simulate user behaviours against test target app.

# How UI Tests support our development
Today, you can tast UI tests and its our story.
I'm happy if anyone has motivation to try ui tests after my talk.

Meanwhile, I don't talk topick about unit test level.

# We should know about the test target if we tast tests
(いまいち...)

We should learn test target if we tast test not only about tools but also strategies.
So, I'll explain about Cookpad and its iOS app at first to help you understand the following topics.

# What is Cookpad?

![](images/what_is_cookpad_world.png)

Cookpad is one of famous recipe sharing service in the world.
We have two kind of the service, for Japan and for rest of the world for now.
According to the similarweb.com, Cookpad is the largest site in food category.

# Cookpad for iOS(Japan and Global)

![](images/cookpad_for_ios_japan.png)
![](images/cookpad_for_ios_global.png)

We also have two kind of iOS applications.
One is for Japan and another is for rest of the world.
They are difference service growth level, so we have't merge them yet.

Anyone comes from out of Japan, can see global app.

# Cookpad for iOS(Japan)

![](images/cookpad_for_ios_global.png)

I focus on japanese app today.

# History for Cookpad iOS App

![](images/history_for_cookpad_ios_image1.png)
![](images/history_for_cookpad_ios_image2.png)
![](images/history_for_cookpad_ios_image3.png)
![](images/history_for_cookpad_ios_image4.png)
![](images/history_for_cookpad_ios_graph.png)

The cookpad app have grown for around 5 years.
I attched some screenshots to be able to check the change.
The app changed UI component/features many times during the period.
In addition, the app changes not only UI but also internal logic, implementatins.
(ここ、いまいち)
Sorce code also have grown and it is around 100 thousand lines except for comment, balnk lines for now.

# Kano-model and Japan market

![](images/kano_model_based_quality.png)

https://en.wikipedia.org/wiki/Kano_model

kano-model is one of famous model to explain about quality.
There is two quality. One is Must-be Quality and another is Attractive Quality.
Japan market's must-be quality is high because they require crash-free app as must-be quality in many case.

# diachronic quality in mobile app

Mobile app's environment changes frequently.
OS version change every year.
UI and design also change a few years cycle.
Required quality by market also have changed.

# Changes in Cookpad

- release cycle: 2week ~ 1months
- change ui / code

In this period, Cookpad also have changed to catch up with the cycle.
Release our app every two weeks or one months to challenge our service and UI.
Recently, we changes source code around 5,000 ~ 10,000 lines per release.

# summary

History of Cookpad iOS app and its changes
diachronic quality in mobile

# Tasting tests😋

I start talking UI Test what I've done for the environment.

# History for UI Tests for Cookpad iOS App

![](images/history_for_ui_tests.png)

This repository show a growth of UI tests I implemented at Cookpad.
I've developed the environment since 2014.
I've supported the changes with this ui tests.

# Why have we implemented this UI tests?

# Re-Engineering

Start tasting tests to re-egnineering.
Especially, I talk about refactor/re-write code.

# Should we taste from?

> Writing unit tests before refactoring is sometimes impossible and often pointless.

According to the re-engineering, the quotation is described.
it is true since we can't check behaviour without tests.
The most of developers may agree with re-write/refactor features without tests lead unexpected broken stuff.
BTW, to make the target app testable, we should consider architecture for the app and other many things.

On the other hand, without CI environment, it is difficult to iterate development cycle quickly without tests.

# Basic strategy for Re-Engineering

  (internal) sorce code => |app| <= (externl) users

In this case, we aproach to make the app testable from two aspect, internal and external.
"Internal" means sorce code side.
"external" means end-user and GUI side.

# Make checkable from external to internal

Check if GUI/behaviour are broken from external.
And re-write/refactor/implement new feature.
Developers continue to change code aggressive because if some feature broken, we can know the bug in gui level.

# Unit tests for Re-Engineering

The re-engineering also describe the following quotation.

> Most developers would agree that unit test should be fully automated,

This also true, for most of developers, I think.

# Unit tests are not a silver bullet

> but the level of automation for other kind of tests(such as integration tests) is often much lower.

This also.

# UI Test to support Re-Engineering

But....

> One area that cries out for automation is UI testing.
> (4.3.2. Regression testing without unit tests)

So, UI tests take too many time and too many human resources in mobile in many case.
Because test automation for mobile is difficult than we app.

But, automated UI tests support re-engineering in many time.
You can check most of views, screen transaction without crashes and so on, automatically.
You can check various OS versions and resolutions without human resorces.

This benefit also lead psychological safety for developers.

# Test environment for Mobile apps tend to be flipped pyramid easily

I shown ideal test pyramid for test automation before.
But in mobile context, it is easy to make it flipped.
Because checking UIs manually is easy than test automation but it block swift development cycle in the future.

# implement the strategy

# Automated UI Test with Appium from 2014

So, I've tried to implement UI Test since 2014, I've joined cookpad.
I run UI tests manually and implement automated test step by step.
I've implemented it with Ruby :p

# Architecture for UI Tests

図にする
|シナリオ| <=> ｜操作の実装｜ <=> internal libraries <=> ruby_lib(appium ruby binding) <=> Appium <=> iOS(UIAutomation/XCUITest) <=> Cookpad App

Our architecture for automated test is like this.
We separate some layer to divide responsibilties for scenarios associated with end users and code associated with iOS framework.

I'd like to independent scenarios from iOS related environment.
Also, I'd like to independent implementations for iOS from user scenarios.

iOS側が変化した時は、シナリオは変えず、internal librariesのところだけでiOSフレームワーク側の変更を吸収します

Thus, we can decrease maintanance costs for user scenarios and changing iOS side.

Separating the responsibility is used for developers.


# Scenarios

This is example to describe scenarios.
I implement scenarios with data driven testing with Turnip.
Turnip is similar to Cucumber.
This scenaro is close to end-user. So, I chose national language to describe test.

This scenario is not equal to test case which run by manually.
I summarize and implement this avoid redundant scenarios.

# Seasoning


# Tips1: reduce dependency with production code
It is important to describe test scenarios independent to internal logic for production code.
For example, the following finding elements on view with XPath will be broken easily if update OS version from iOS7 to iOS8.

```
find_element :xpath, //UIAApplication[1]/UIAWindow[1]/UIATableView[1]/UIATableCell[1]
```

So, it is better to implement with accessibilityIdentifier or accessibilityLabel.

```
find_element :accessibility_id, "arbitrary identifier"
```

Keep independency with scenarios and internal logic for production is also important for this level's tests.
(BTW, this point also important for development.)

# tips2: Don't run tests for all boundaries
test for all boundaries is better to implement in unit test.
because UI test is too slower than unit test.
So, if we implement some boundaries in UI test side, it is better to move test from ui to unit and remove it from ui tests in the future.

# more 🌶️

To be advanced, we implement this library in the future.

we also implement image diff to judge the result and feedback to designer.
Designer can know the diff between previous version and new version quickly.
This help check simple changes in views.


And we also capture network traffic because we'd like to check logging request.
Logging reqest is so important for service development.

# Re-Engineering - re-write / re-factor without fear for developers
Keeping this UI tests, developers re-write and refactor internal code and they introduce new test.
If therir change broke some feature, UI tests can unclear the error because our tests cover around 80~90% screen transactions for now.

# introduce Swift
We start to introducing Swift a few months ago.
Also in this case, UI tests help fearless changes for developers.

# faster and more stable
Current UI tests is enough for current our development process for now.
But our team will bigger than now in the future.
So, I'll introduce alternative tools such as XCUITest or EarlGrey for UI tests parcially.
I think that we continue to use both Appium and EarlGrey but we separate them by responsibilities.

# Conclusion
I talked about history of cookpad and how try to re-engineer the big app with UI tests.
UI tests need to selarate responsibility from product code to catch up with some changes painless.

# Thanks
Thanks for listening my talk.
And our co-workers.
今日の話は、チーム全体として動かないとうまくいかないものだった。

