---

copyright:
  years: 2020
lastupdated: "2020-04-29"

keywords: mobile analytics, instrumenting android app

subcollection:  mobilefoundation-sw

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:term: .term}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:external: target="_blank" .external}

# Add {{site.data.keyword.mobilefoundation_short}} Analytics
{: #instrument_your_app_android}

{{site.data.keyword.mobileanalytics_short}} provides key application usage and application performance insights for mobile application developers and application owners.

You need to instrument your mobile application to use the {{site.data.keyword.mobileanalytics_short}} feature to monitor your application usage, performance and to get other statistics. 
Instrumenting you application has the following steps:

1. Import and install the Mobile Analytics Client SDK.
1. Instrument your application based on the type of analytics data you want to collect.

## Instrument your Android application
{: #instrument_android_app}

### Step 1: Import and install the {{site.data.keyword.mobileanalytics_short}} Client SDK for Android
{: #install_analytics_sdk_android}
[![Maven Central-mfp](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobile.foundation/ibmmobilefirstplatformfoundation/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobile.foundation/ibmmobilefirstplatformfoundation){: external}
[![Maven Central-mfp Analytics](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobile.foundation/ibmmobilefirstplatformfoundationanalytics/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobile.foundation/ibmmobilefirstplatformfoundationanalytics){: external}

The {{site.data.keyword.mobileanalytics_short}} Client SDK is distributed with Gradle, a dependency manager for Android projects. Gradle automatically downloads artifacts from repositories and makes them available to your Android application.

1. Create an [Android Studio](http://developer.android.com/sdk/index.html){: external} project or open an existing project.

2. Open the `build.gradle` file that is in your **app module**.

   Your Android project might have two `build.gradle` files: one for the project and one for the app module. Make sure to use the **app module** file.
   {: tip}

3. Find the `Dependencies` section of the `build.gradle` file and add a compile dependency for the {{site.data.keyword.mobileanalytics_short}} Client SDK. Your repositories statement must be similar to the following code example:

   ```
   dependencies {
     compile 'com.ibm.mobile.foundation:ibmmobilefirstplatformfoundation:8.0.+'
     compile 'com.ibm.mobile.foundation:ibmmobilefirstplatformfoundationanalytics:8.0.+@aar'
     // other dependencies
   }
   ```
   {: codeblock}

   The first dependency is for the {{site.data.keyword.mobileanalytics_short}} client sdk for capturing and logging application [runtime](#x2391929){: term} events and the second dependency is for enabling in-app user feedback interacting with the application user. The second dependency is only required if you enable in-app user feedback.

4. Synchronize your project with Gradle by clicking **Tools &gt; Android &gt; Sync Project with Gradle Files**.

5. Open the `AndroidManifest.xml` file for your Android project. You can find this file in **app > manifests**. Add internet access and location access permission under the `<manifest>` element:

   ```xml
   <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}

   If you're using SDK version greater than >= 1.2, then you need to put the following lines inside the `<application>` element of the `AndroidManifest.xml` file.

   ```
   <activity
   android:name="com.ibm.mobilefirstplatform.clientsdk.android.ui.UIActivity"
   android:label="@string/app_name"
   android:launchMode="singleTask">
   <intent-filter>
   <action android:name="android.intent.action.MAIN" />
   <category android:name="android.intent.category.LAUNCHER" />
   </intent-filter>
   </activity>
   ```
   {: codeblock}

### Step 2: Instrument your Android application based on the type of analytics data you want to collect
{: #instrument_app_based_on_data_android }

1. Initialize your application to capture and send analytics data to {{site.data.keyword.mobileanalytics_short}} service. First, add the following `import` statements to the beginning of your application or activity class:

   ```Java
   import com.worklight.common.Logger;
   import com.worklight.common.WLAnalytics;
   ```
   {: codeblock}

   Next, use the Mobile Analytics Client SDK to set up or initialize the capture of analytics data. 

   Add the initialization code in the `onCreate` method of the main activity in your Android application, or in a location that works best for your application project.
   {: android}

   ```Java
   WLAnalytics.init(this.getApplication());
   ```
   {: codeblock}

   Before calling the init method, you must ensure that your application embeds the required code to authenticate and authorize the device with the {{site.data.keyword.mobilefoundation_short}} service. This step is a common step that is required of all {{site.data.keyword.mobilefoundation_short}} services applications and is not specific to Analytics data capture. <!--  Refer <need to link doc that talks about auth> -->

   With initialization complete, your application is now enabled to capture device information and {{site.data.keyword.mobileanalytics_short}} SDK logs with no further code added. Any further APIs and code that is discussed in the following sections is optional and can be added based on what sort of analytics data you want to capture.

2. To capture application lifecycle events such as application session and crash information, configure your application by adding the following line of code:

   ```Java
   WLAnalytics.addDeviceEventListener(WLAnalytics.DeviceEvent.LIFECYCLE);
   ```
   {: codeblock}

3. To capture network events that capture the applications network interactions, configure your application by adding the following line of code:

   ```Java
   WLAnalytics.addDeviceEventListener(WLAnalytics.DeviceEvent.NETWORK);
   ```
   {: codeblock}

4. You now initialized your application to capture analytics data. Next, you must send the captured data to the {{site.data.keyword.mobileanalytics_short}} service.

   Use the following API to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service.

   ```java
   WLAnalytics.send();
   ```
   {: codeblock}

   You are free to decide when to call this API in your application flow to send the captured analytics data to the {{site.data.keyword.mobileanalytics_short}} service. Until this sends, all captured analytics data is stored locally on the device.

5. To capture and send application logs to the Mobile Analytics service, use the {{site.data.keyword.mobileanalytics_short}} Client SDK logger APIs. 

   The {{site.data.keyword.mobileanalytics_short}} Client SDK logging [framework](#x2023472){: term} supports the following log levels, which are listed from least to most verbose, with recommended use guidelines:

   * FATAL - Use for unrecoverable crashes or hangs. The FATAL level is reserved for logging unrecoverable errors, which appear to users as an application crash
   * ERROR - Use for unexpected exceptions or unexpected network protocol errors
   * WARN - Use to log usage warnings that aren’t considered critical errors, such as usage of deprecated APIs or slow network response
   * INFO - Use for reporting initialization events and other data that might be important, but not urgent
   * DEBUG - Use for reporting debug statements to help developers resolve application defects.

   When the logger level is set DEBUG, you also get Mobile Analytics Client SDK logs, which are included when you send logs.
   {: note}

   The following code snippets show sample Logger usage for Android:

   ```java
   // Set the logging level (optional)
   // The default setting is Logger.LEVEL.DEBUG
   Logger.setLogLevel(Logger.LEVEL.INFO);

   //Create a logger instance. You can create multiple loggers to organize your logs as you wish
   Logger logger = Logger.getInstance("loggerName");

   // Log messages with different levels
   // Debug message for feature 1
   // Info message for feature 2
   logger.debug("debug message");
   //the logger.debug message is not logged because the logLevelFilter is set to Info
   logger.info("info message");

   // Send logs to the Mobile Analytics
   Logger.send();
   ```
   {: codeblock}

6. To get insights on user onboarding patterns (new users versus returning users), you must associate a user identity with your application session. This step can be done by calling the following API:

   ```java
   WLAnalytics.setUserContext("userName or userIdentity");
   ```
   {: codeblock}

   All analytics data that is captured and stored locally is sent to the Mobile Analytics service only when the WLAnalytics.send() API is called.

7. To get insights into your applications HTTP network interaction patterns such as HTTP APIs called, number of requests and average response times you must use the {{site.data.keyword.mobilefoundation_short}} Service Client SDK's WLResourceRequest class to make the HTTP calls. Although you initialized Analytics for the capture of Network events, by using `WLResourceRequest` enables the {{site.data.keyword.mobileanalytics_short}} to hook into the network calls and capture the relevant data. Make your HTTP calls as in the following code.

   ```java
   WLResourceRequest request = new WLResourceRequest(new URI(url), WLResourceRequest.GET);
         request.send(new WLResponseListener() {

             @Override
             public void onSuccess(WLResponse wlResponse) {
                 //handle success of HTTP call and use wlResponse
             }

             @Override
             public void onFailure(WLFailResponse wlFailResponse) {
                 //handle failure of HTTP call and use wlFailResponse
             }
         });
   ```
   {: codeblock}

8. To get Crash Analytics and logs, you might call the following the API during start of your application to check whether the previous session fails and send the capture crash logs to the {{site.data.keyword.mobileanalytics_short}} service.

   ```java
   if (Logger.isUnCaughtExceptionDetected()) {
         //add any other handling you may want and call the following APIs
         WLAnalytics.send();
         Logger.send();
   }
   ```
   {: codeblock}

9. To define Custom Analytics and define your own analytics data over what is supported inherently in the Client SDK, you might use the custom logging API

   ```java
   //create a JSON to capture the custom data
   JSONObject jsonObject = new JSONObject();
   jsonObject.put("FromPage", "LoginPage");

   //log the custom data with a message
   WLAnalytics.log("log message", jsonObject);

   //Send the captured custom data and log to the Mobile Analytics service
   WLAnalytics.send();
   ```
   {: codeblock}

   The logged custom data can be plotted over custom charts you can define in the Mobile Analytics console to derive custom insights.

10. Use In-App User Feedback to deepen your application performance analysis. You can enable your application **users and testers** to provide rich contextual feedback to the app owners. **App owners** get real-time feedback from its users on the application usage experience which **App owners** and **Developers** can further act on. This feature brings in significant agility to application up-keep. Use the following API to switch your application to Interactive Feedback Mode in any action handler in your application, for example, when you handle the click of a button or the selection of a menu item.

   ```java
   WLAnalytics.triggerFeedbackMode();
   ```
   {: codeblock}

## What to do next?
{: #next_steps_analytics_android}

Try a simple sample from [here](https://github.com/MobileFirst-Platform-Developer-Center/mfp-analytics-samples/tree/release80/android){: external}. In less than 5 minutes, you can run the sample application and get a feel of what the API does. You can also notice how analytics shows up as different insights on the Analytics console. 

{{site.data.keyword.mobilefoundation_short}} Analytics Service provides [REST](#x3220987){: term} APIs to help developers with importing (POST) and exporting (GET) analytics data.

For more Analytics tutorials, see {{site.data.keyword.mobilefoundation_short}} documentation [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/){: external}.
{: note}

You can also learn to do the following.

* [Configure offline storage](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-configure_offline_storage_android).
* [Send in-app feedback](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-sending_in_app_user_feedback_android).
* [Receive Push Notifications](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-receiving_push_notifications_in_android).

