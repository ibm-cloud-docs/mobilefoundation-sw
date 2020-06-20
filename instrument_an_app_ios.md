---

copyright:
  years: 2020
lastupdated: "2020-04-29"

keywords: mobile analytics, instrumenting iOS app

subcollection:  mobilefoundation-sw

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:term: .term}
{:important: .important}
{:note: .note}
{:download: .download}
{:external: target="_blank" .external}

# Add {{site.data.keyword.mobilefoundation_short}} Analytics
{: #instrument_your_app_ios)

{{site.data.keyword.mobileanalytics_short}} provides key application usage and application performance insights for mobile application developers and application owners.

You need to instrument your mobile application to use the {{site.data.keyword.mobileanalytics_short}} feature to monitor your application usage, performance and to get other statistics. 
Instrumenting you application has the following steps:

1. Import and install the Mobile Analytics Client SDK.
1. Instrument your application based on the type of analytics data you want to collect.

## Instrument your iOS application
{: #instrument_ios_app}

Steps to instrument your iOS application:

### Step 1: Import and install the Mobile Analytics Client SDK for iOS
{: #install_analytics_sdk_ios}

[![CocoaPods Compatible - {{site.data.keyword.mobilefoundation_short}}](https://img.shields.io/cocoapods/v/IBMMobileFirstPlatformFoundation.svg)](https://cocoapods.org/pods/IBMMobileFirstPlatformFoundation){: external}
[![CocoaPods Compatible - {{site.data.keyword.mobileanalytics_short}}](https://img.shields.io/cocoapods/v/IBMMobileFirstPlatformFoundationAnalytics.svg)](https://cocoapods.org/pods/IBMMobileFirstPlatformFoundationAnalytics){: external}

The Swift SDK is available for iOS and watchOS.

1. Add the following to the existing podfile, which is at the root of the Xcode project

   ```bash
   use_frameworks!
   platform :ios, 8.0
   target "ProjectName" do
       pod 'IBMMobileFirstPlatformFoundation'
       pod 'IBMMobileFirstPlatformFoundationAnalytics'
   end
   ```
   {: codeblock}

2. From a Command-line window, go to the root of the Xcode project and run the following command

   ```bash
   pod update
   ```
   {: codeblock}

### Step 2: Instrument your iOS application based on the type of analytics data you want to collect
{: #instrument_app_based_on_data_ios}

3. Initialize your application to enable sending logs to the Mobile Analytics.
   The Swift SDK is available for iOS and watchOS. Import the `BMSCore` and `BMSAnalytics` [frameworks](#x2023472){: term} by adding the following `import` statements to the beginning of your `AppDelegate.swift` project file:

   ```Swift
   import IBMMobileFirstPlatformFoundation
   ```
   {: codeblock}

   Next, use the Mobile Analytics Client SDK to set up or initialize the capture of analytics data.
   Add the initialization code in a location that works best for your application project.

   ```Swift
   WLAnalytics.init()
   ```
   {: codeblock}

   Before you call the init method, you must ensure that your application embeds the required code to authenticate and authorize the device with the MobileFoundation service. This step is a common step that is required of all {{site.data.keyword.mobilefoundation_short}} services applications and is not specific to Analytics data capture. <!--  Refer <need to link doc that talks about auth> -->

   With initialization, complete your application is now enabled to capture device information and Mobile Analytics SDK logs with no further code added. Any further APIs and code that is discussed in the following sections is optional and can be added based on what sort of analytics data you want to capture.

4. To capture application lifecycle events such as application session and crash information configure your application by adding the following line of code:

   ```Swift
   WLAnalytics.sharedInstance().addDeviceEventListener(LIFECYCLE)
   ```
   {: codeblock}

5. To capture network events that capture the applications network interactions, configure your application by adding the following line of code:

   ```Swift
   WLAnalytics.sharedInstance().addDeviceEventListener(NETWORK)
   ```
   {: codeblock}

6. You now initialized your application to capture analytics data. Next, you must send the captured data to the Mobile Analytics service.
   Use the following API to send analytics data to the Mobile Analytics service.

   ```Swift
   WLAnalytics.sharedInstance().send();
   ```
   {: codeblock}

   You are free to decide when to call this API in your application flow to send the captured analytics data to the Mobile Analytics service. Until this, send all captured analytics data is stored locally on the device.

7. To capture and send application logs to the Mobile Analytics service, use the Mobile Analytics Client SDK logger APIs.
   The Mobile Analytics Client SDK logging framework supports the following log levels, which are listed from least to most verbose, with recommended use guidelines:
   * FATAL - Use for unrecoverable crashes or hangs. The FATAL level is reserved for logging unrecoverable errors, which appear to users as an application crash
   * ERROR - Use for unexpected exceptions or unexpected network protocol errors
   * WARN - Use to log usage warnings that aren’t considered critical errors, such as usage of deprecated APIs or slow network response
   * INFO - Use for reporting initialization events and other data that might be important, but not urgent
   * DEBUG - Use for reporting debug statements to help developers resolve application defects.

   When the logger level is set DEBUG, you also get Mobile Analytics Client SDK logs, which are included when you send logs.
   {: note}

   Follow [the tutorial](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/application-development/client-side-log-collection/ios/){: external} for code snippets for Logger to add logging capabilities in iOS applications.

8. To get insights on user onboarding patterns (new users versus returning users), you must associate a user identity with your application session. This association can be done by calling the following API:

   ```Swift
   WLAnalytics.sharedInstance().setUserContext("userName or userIdentity")
   ```
   {: codeblock}

   All analytics data that is captured and stored locally is sent to the Mobile Analytics service only when the `WLAnalytics.sharedInstance().send()` API is called.

9. To get insights into your applications HTTP network interaction patterns such as HTTP APIs called, number of requests and average response times you must use the {{site.data.keyword.mobilefoundation_short}} Service Client SDK's WLResourceRequest class to make the HTTP calls. Although you initialized Analytics for the capture of Network events, the use of  `WLResourceRequest` enables the Mobile Analytics to hook into the network calls and capture the relevant data. Make your HTTP calls as in the following code.

   ```Swift
   let request = WLResourceRequest( url: URL(string: "/adapters/JavaAdapter/users"), method: WLHttpMethodGet )

   request!.send { (response, error) -> Void in
       if(error == nil){
           //handle failure of HTTP call and use wlFailResponse
       }
       else{
           //handle success of HTTP call and use wlResponse
       }
   }
   ```
   {: codeblock}

10. To get Crash Analytics and logs, you might call the following the API during start of your application to check whether the previous session fails and send the capture crash logs to the Mobile Analytics service.

   ```Swift
   if (OCLogger.isUnCaughtExceptionDetected()) {
         //add any other handling you may want and call the following APIs
         WLAnalytics.sharedInstance().send();
         OCLogger.send();
   }
   ```
   {: codeblock}

11. To define Custom Analytics and define your own analytics data over what is supported inherently in the Client SDK, you might use the custom logging API

   ```Swift
   //create an array object with key value pair as custom data
   let eventObject = ["FromPage": "LoginPage"]

   //log the custom data with a message
   WLAnalytics.sharedInstance().log("log message", withMetadata: eventObject);

   //Send the captured custom data and log to the Mobile Analytics service
   WLAnalytics.sharedInstance().send();
   ```
   {: codeblock}

   The logged custom data can be plotted over custom charts you can define in the Mobile Analytics console to derive custom insights.

12. Use In-App User Feedback to deepen your application performance analysis. You can enable your application **users and testers** to provide rich contextual feedback to the app owners. **App owners** get real-time feedback from its users on the application usage experience which **App owners** and **Developers** can further act on. This feature brings in significant agility to application up-keep. Use the following API to switch your application to Interactive Feedback Mode in any action handler in your application, for example, when you handle the click of a button or the selection of a menu item.

   ```Swift
   WLAnalytics.sharedInstance().triggerFeedbackMode();
   ```
   {: codeblock}

## What to do next?
{: #next_steps_analytics_ios}

Try a simple sample from [here](https://github.com/MobileFirst-Platform-Developer-Center/mfp-analytics-samples/tree/release80/ios){: external}. In less than 5 minutes, you can run the sample application and get a feel of what the API does. You can also notice how analytics shows up as different insights on the Analytics console. 

{{site.data.keyword.mobilefoundation_short}} Analytics Service provides REST APIs to help developers with importing (POST) and exporting (GET) analytics data.

For more Analytics tutorials, see {{site.data.keyword.mobilefoundation_short}} documentation [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/){: external}.
{: note}

You can also learn to do the following.

* [Configure offline storage](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-configure_offline_storage_ios).
* [Send in-app feedback](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-sending_in_app_user_feedback_ios).
* [Receive Push Notifications](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-receiving_push_notifications_in_ios).
