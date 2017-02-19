# Tasting tests at Cookpad
@Kazu_cocoa

Hello everyone.
I'm Kazu.
Now, I'm so happy and exciting to be able to talk for many Swift and iOS develpers.

Today's my topic is associated with "TEST" since I'm test engineer at Cookpad.
"Tasting" used in my title means taste food stuff because my company is regarding with food.

# About me

First, I talk myself.
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

# What I talk for now

History of Cookpad iOS app and its changes
diachronic quality in mobile

# Tasting tests😋

I start talking UI Test what I've done against the environment.

# History for UI Tests against Cookpad iOS App

![](images/history_for_ui_tests.png)

This repository show a growth of UI tests I implemented at Cookpad.
I've developed the environment since 2014.
I've supported the changes with this ui tests.

# Re-Engineeringを進める

# どこからテストを拡充していくか?


# Why have we implemented this UI tests?


# Basic strategy for Re-Engineering


# 内部を変更できるようにするために、外部からカバーしていく

# Unit tests for Re-Engineering


# Unit tests are not a silver bullet


# UI Test to support Re-Engineering


# Test environment for Mobile apps tend to be flipped pyramid easily

# implement the strategy

# Automated UI Test with Appium from 2014


# Architecture for UI Tests


# Scenarios


# what kind of scenarios do we describe


# Seasoning


# Tips1: 内部コードから依存性を減らす


# Tips2: 環境変数によりテスト対象の挙動を帰る


# Tips3: set accessibilityIdentifier with code/storyboard


# tips4: データの境界値は網羅しない


# Tips5: 要素のタップベースでシナリオを書く


# more 🌶️


# Re-Engineering - re-write / re-factor without fear for developers


# introduce Swift


# faster and more stable


# Conclusion

# Thanks
