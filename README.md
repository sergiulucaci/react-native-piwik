Piwik SDK for React Native
========================

This document describes how to get started using the Piwik Tracking SDK for React Native. 
[Piwik](http://piwik.org) is the leading open source web analytics platform 
that gives you valuable insights into your website's visitors, 
your marketing campaigns and much more, so you can optimize your strategy and experience of your visitors.
This relies on the native [Android SDK](https://github.com/piwik/piwik-sdk-android) and on the native [iOS SDK ](https://github.com/piwik/piwik-sdk-ios) for Piwik and this README page is heavily inspired by it.

## Getting started

Integrating Piwik into your React Native app
 
1. [Install Piwik](http://piwik.org/docs/installation/)
2. [Create a new website in the Piwik web interface](http://piwik.org/docs/manage-websites/). Copy the Website ID from "Settings > Websites".
3. [Include the library](#include-library)
4. [Initialize Tracker](#initialize-tracker).
5. [Track screen views, goals and more](#tracker-usage).


### Include the library

#### iOS

1. Add `node_modules/react-native-piwik/ios/BNFPiwik.xcodeproj` to your xcode project, usually under the `Libraries` group
2. Add `libBNFPiwik.a` (from `Products` under `BNFPiwik.xcodeproj`) to build target's `Linked Frameworks and Libraries` list
3. Delete `piwiktracker.xcdatamodeld`(from `Libraries` under `BNFPiwik.xcodeproj/PiwikTracker`)
4. Drag `node_modules/react-native-piwik/ios/PiwikTracker/piwiktracker.xcdatamodeld` into the folder containing `AppDelegate.m`

#### Android
- Open `/android/settings.gradle`
- Below `include ':app'` add:

```
include ':react-native-piwik'
project(':react-native-piwik').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-piwik/android/') 
```
- Open `android/app/build.gradle`
- Add the following under `dependencies`:

```
compile project(':react-native-piwik')
```
- Open your `MainApplication.java` file under `android/src`
- Import the lib using `import de.bonify.reactnativepiwik.PiwikPackage;`
- Add the following `new PiwikPackage()` to the `getPackages` function.


### Tracker Usage

#### Init tracker

Before using any function below, the tracker must be initialized.

```javascript
Piwik.initTracker("https://your-piwik-domain.tld/piwik.php", 1)
```
#### Set User ID

Providing the tracker with a user ID lets you connect data collected from multiple devices and multiple browsers for the same user. A user ID is typically a non empty string such as username, email address or UUID that uniquely identifies the user. The User ID must be the same for a given user across all her devices and browsers. .
If user ID is used, it must be persisted locally by the app and set directly on the tracker each time the app is started.

If no user ID is used, the SDK will generate, manage and persist a random id for you.
```javascript
Piwik.setUserId("123e4567-e89b-12d3-a456-426655440000")
```

#### Track screen views

To send a screen view set the screen path and titles on the tracker.

```javascript
Piwik.trackScreen("/your_activity", "Title")
```

#### Track events

To collect data about user's interaction with interactive components of your app, like button presses or the use of a particular item in a game 
use trackEvent.

```javascript

Piwik.trackEvent("category", "action", "label", 1000)
```

#### Track goals

If you want to trigger a conversion manually or track some user interaction simply call the method trackGoal. Read more about what is a [Goal in Piwik](http://piwik.org/docs/tracking-goals-web-analytics/).

```javascript

Piwik.trackGoal(1, revenue)
```


#### Track App Downloads

If you want to track the app downloads, there is also a function to do that (only supported on Android).
```javascript

Piwik.trackAppDownload()
```

#### Setting App Opt Out

The PiwikTracker SDK supports opting out of tracking. Note that this flag must be set each time the app starts up and will default to false. To set the app-level opt out, use:
```javascript

Piwik.setAppOptOut(true);
```

## Contribute

* Fork the project
* Create a feature branch based on the 'master' branch
* Create a PR and feel proud.



## License

react-native-piwik is released under the MIT license, see [LICENSE](https://github.com/BonifyByForteil/react-native-piwik/blob/master/LICENSE).

