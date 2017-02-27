# Tasting tests at Cookpad

Hello, everyone.
I'm Kazu.
I'm so excited talking for many Swift and iOS developers.

Today, I will talk about "TEST" since I'm a test engineer.
I used “tasting” in my title because my company is food-related.

# about me

At first, I will introduce myself.
I'm Kazuaki Matsuo and working at Cookpad as a test engineer and Software Engineer in Quality.
I've tried test automation for mobile and improved development processes and other some roles to improve several qualities for our services.

I develop with some languages in my work such as swift, ruby, java for android and elixir.
Recently, I’m maintaining ruby appium binding.
Appium is one of the famous mobile test automation tools.

# 😋

let’s go Cooking!

# A bunch of themes in tests

Even we use the word "TEST", it has a bunch of themes and various meanings.
For example, it has categories such as usability test and performance test, and test level such as unit test and integration test, and so on.

Today, I pick up test level and a test pyramid associated with test automation.


# How UI Tests support our development

I focus on UI tests and how the tests support our development.
I won’t talk about unit/integration level tests today.

So, you can taste how UI tests support our development and the strategy in our app as a case study.

I'm happy if anyone gets the motivation to consider test strategy for your app and try UI tests after my talk.

# We should know about the test target
Before starting to talk about tests, I’ll explain about a test target.
Because knowledge for the test target help you understand test strategies and  today’s case study.

So, I explain about Cookpad and its iOS app at first.

# What is Cookpad?
Cookpad is one of the most famous recipe sharing services in the world.

# simularweb.com

According to the similarweb.com, Cookpad is the largest site worldwide in the food category.

Currently, we provide our services for Japan and countries around the world.


# Cookpad for iOS(Japan and Global)

We also have two kinds of iOS app.
One is for Japan and another is for rest of the world.
Their service growth level is different, so we haven't merged them yet.

The Global application can be downloaded from any non-Japanese app Store.

# Cookpad for iOS(Japan)

Today’s main target is for Japan Edition.

# The app has been developed for a long time

The Japan edition has grown for around 5 years.
I attached some screenshots to show the growth and the changes.

The app changed UI component, add or delete any features or re-write/refactor implementations during the period.

The production code also has grown and it is around one hundred thousand lines excluding
 for comment, blank and new lines right now.

# How often Cookpad app changes

In this period, we’ve release the app many times.

Recent our release cycle is from around 2weeks to one month.
We change source code from around 5 thousand to 10 thousand per release.

The changes have some new features, GUI update, refactor/re-wrote internal logic and so on.

# kano-model and Japan market
by the way, I also explain a bit about quality.
kano-model is one of the famous models to explain about quality.
The model has two main quality.
One is Must-be Quality and another is Attractive Quality.
Must-be quality is a criteria you must satisfied with basic needs.

Must-be quality in Japan have required crash-free app for almost views and no degrade features for a long time.
So, we had needed to keep crash-free conditions in our development.
It is not attractive for them.

# Diachronic Quality for Mobile
Mobile app's environment have been changed quickly through time.
OS versions, UI, design, user experience, required quality by market and so on.

Recently, I sometimes mention such a movement as diachronic quality.
This word is influenced by linguistics.
Diachronic means something has developed and evolved through time.

A bunch of mobile environments have changed through time.

# take a break 🍵

I talked histories of Cookpad iOS app and how long the app has developed for a long time.
In addition, I talked a bit about quality for japan market and mobile.

# Tasting how re-engineering the app with UI Tests😋

I start talking how we implement and conduct UI Tests to proceed re-engineering our app.

# A History for UI Tests for Cookpad Apps

This repository shows a growth of UI tests I’ve implemented at Cookpad.
I've developed the environment since 2014.

#  Why have we implemented  this UI tests?🤔
In 2014, We expected our service need to develop continuously and we should evolve apps in the future.
So, we needed to proceed re-engineering for our mobile apps.

Re-engineering means re-structured the target and make it testable to be able to develop stuff continuously without degrade features and keep development speed and so on.

# Should we taste from?

> Writing unit tests before refactoring is sometimes impossible and often pointless.

This sentence is quoted from "Re-Engineering Legacy Software".
It is true since we can't check behaviour without tests.

The most of the developers may agree with re-write/refactor features without tests lead unexpected broken stuff.
In addition, to make the target app testable, we should consider architectures for the app and other many things if target app isn't testable.

On the other hand, without CI environment, it is difficult to iterate development cycle quickly without tests.

# Basic strategy

We approached to proceed re-engineering the app from two aspects, internal and external.
"Internal" means production code side.
"External" means end-user and GUI side.

# Make checkable from external to internal
I explain a cycle.

Check whether GUI, behaviour are broken from external.

And re-write/refactor/implement some features and implement unit tests.

Check the changes from UI side to uncover errors.
Developers can find some bugs if their implementations break some other features unexpected.


If tests uncover some bugs, we can fix the issue before release.
This kind of UI level checking is not only automated tests but also manual checking.

# Unit tests for Re-Engineering

The re-engineering also describes the following quotation.

> Most developers would agree that unit test should be fully automated,

I think most of the developers agree with this.

# Unit tests are not a silver bullet
But, it also describes as...

> but the level of automation for other kind of tests(such as integration tests) is often much lower.

Certainly, implementing automated tests for integration and UI layer is difficult than unit layer especially mobile app.

# UI Test should be automated
But...

> One area that cries out for automation is UI testing.

yes, automated UI testing is very important.

In many cases, UI tests take too much time and too many human resources in mobile because test automation for mobile is difficult.
UI tests for mobile tend to conducted by manual.


# Test Pyramid

I talked the ideal test pyramid for test automation before.
This shows unit tests are the largest and UI tests are the smallest.

# Flipped pyramid make development cycle slow
But in the mobile context, it is easy to make it flip.


Checking UIs manually is easy than test automation.
But large manual tests block swift development cycle in the future.

So, converting manual checking to automated UI tests and increase unit tests is very important.

If you succeed increasing automated UI tests, you can check automatically most of the layouts, screen transactions and so on.


# Conduct tests for combinations

You can also check combinations of various OS versions and resolutions without additional human resources.

Certainly, designing test architecture for test automation is also important.
Don't convert all manual tests to dirty automated tests.

# implement the strategy

# We’ve been developed UI Tests since 2014

We’ve been developed UI Tests since 2014 to support re-engineering.
At first, we had many manual tests and no automated UI tests.
But currently, we have many UI Tests which cover around 80% screen transactions, and spot manual testing.

# Architecture for UI Tests

Our architecture for the automated test is like this.
We separate some layer to divide responsibilities for scenarios associated with end-users and product code associated with the iOS framework.

This architecture keeps independence between end-user scenarios and concrete implementations depends on iOS framework.

Thus, we can decrease maintenance costs for scenarios side and iOS side.

I think separating responsibility is familiar to developers.

# Scenarios with data-driven testing

This is an example to describe scenarios.
I implement scenarios with data-driven testing style with Turnip.
Turnip allow us to describe tests with natural languages.
This scenario is close to end-user.
So, I chose the national language to describe the scenarios.

# steps/wrapper/bindings

This is steps and wrappers to convert national language to programming language.
This example is implemented by Ruby.

These two layers are foundations for UI tests.

# 🍛Seasoning🍲
I share some tips to season the tests.

# Reduce dependency from internal product code

It is important to describe test scenarios independent of internal logic for production code.
For example.
This find_elements method try to find out elements with XPath.
XPath indicate view hierarchy(háɪ(ə)rɑ̀ːrki).
But this finding elements will be broken easily if OS version is updated.


Because the path strongly depends on the iOS framework’s logic.

So, use accessibilityIdentifier or label to avoid this kind of cause.

# Don't conduct tests for all boundaries in UI Tests

Test for all boundaries is better to implement in the unit test.
Because UI test is too slower than the unit test.
So, if you implement all boundaries in UI side, it is better to move tests from UI to unit, and remove it from UI side in the future.

# more 🍛🌶️

More spice to extend UI tests.

I just explain about scenarios and its implementations for UI tests.
But UI tests is not only scenarios but also judgement results and other tips.


# image diff
for example, we also implement image diff to judge the results and feedback to designers.
Designers can know the differences between the previous version and new version easily.
This helps layout checking.

This example shows the diff on systems alert.
The diff was caused only for iOS8.1 when we refactored some internal code before.

# Request counts

And we also capture network traffic for particular scenarios to uncover unexpected requests in them.

We can uncover unexpected burst request with this.


# Re-Engineering re-write/re-factor without fear for developers

Keeping this kind of UI tests and other spices encourage developers re-write and refactor and introduce new tests in unit level.

If their changes broke some features, UI tests can uncover the errors because our UI tests cover around 80% screen transactions.

# introduce Swift

We start to introducing Swift into the app a few months ago.
Near 30% code is already implemented in Swift.


Also in this case, tests make developer confident changes for developers in UI/request level.


# faster🚴 and more stable
Current UI tests are enough for current our development process.
But our team will become bigger than now in the future.
So, I'll introduce alternative tools such as XCUITest or EarlGrey for UI tests partially.
But we don't stop using Appium because their responsibility area and test framework’s lifecycle is different.

# Conclusion

I talked about histories of cookpad app and how we've tried to re-engineering the big app with automated UI tests.
UI tests need to separate responsibility from production code to catch up with some changes painless.

# Do you get motivations to challenge automated UI Tests? 🙌

# Don’t forget this kind of challenges can’t do in developer’s spare time
But don’t forget this kind of challenges can’t do in developer’s spare time.
Certainly, some required skills are similar for each other.
But software test and test automation needs a bit different skills and techniques.


# Thanks
Thanks for listening my talk.



