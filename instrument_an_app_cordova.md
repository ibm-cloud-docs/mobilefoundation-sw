---

copyright:
  years: 2020
lastupdated: "2020-04-29"

keywords: mobile analytics, instrumenting Cordova app

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
{:download: .download}
{:external: target="_blank" .external}

# Add {{site.data.keyword.mobilefoundation_short}} Analytics
{: #instrument_your_app_cordova}

{{site.data.keyword.mobileanalytics_short}} provides key application usage and application performance insights for mobile application developers and application owners.

You need to instrument your mobile application to use the {{site.data.keyword.mobileanalytics_short}} feature to monitor your application usage, performance and to get other statistics. 
Instrumenting you application has the following steps:

1. Import and install the Mobile Analytics Client SDK.
1. Instrument your application based on the type of analytics data you want to collect.

## Instrument your Cordova application
{: #instrument_cordova_app}

Steps to instrument your Cordova application:

### Step 1: Import and install the Foundation and Analytics Client SDK plug-in for Cordova
{: #install_analytics_sdk_cordova }
Instrument your mobile application by using the Mobile Analytics Cordova plug-in.

#### Installing the Cordova Client SDK
{: #install_cordova_sdk}

1. Create a [Cordova](http://cordova.apache.org/#getstarted){: external} project or open an existing project.

2. Add Android or iOS platforms of your choice to your Cordova application. Run one or both of the following commands from the command line.<br/>
   **Android**:
   ```
   cordova platform add android
   ```
   {: codeblock}

   **iOS**:
   ```
   cordova platform add ios
   ```
   {: codeblock}

1. Add the Foundation client sdk plug-in `cordova-plugin-mfp`.
   ```bash
   cordova plugin add cordova-plugin-mfp
   ```
   {: codeblock}

1. Add optional Analytics client sdk plug-in `cordova-plugin-mfp-analytics` that is for in-app feedback capability to your app
   ```bash
   cordova plugin add cordova-plugin-mfp-analytics
   ```
   {: codeblock}

1. Verify that the plug-in installed successfully by running the following command:
   ```bash
   cordova plugin list
   ```
   {: codeblock}

### Step 2: Instrument your Cordova application based on the type of analytics data you want to collect
{: #instrument_app_based_on_data_cordova }

1. In Cordova applications, no setup is required and initialization is built in.

   Before you call any of the following analytic methods, you must ensure that your application embeds the required code to authenticate and authorize the device with the {{site.data.keyword.mobilefoundation_short}} service. This step is a common step that is required of all {{site.data.keyword.mobilefoundation_short}} services applications and is not specific to Analytics data capture. <!--  Refer <need to link doc that talks about auth> -->

   With initialization, complete your application is now enabled to capture device information and {{site.data.keyword.mobileanalytics_short}} SDK logs with no further code added. Any further APIs and code that is discussed in the following sections is optional and can be added based on what sort of analytics data you want to capture.

1. To enable the capture of the lifecycle events, it must be initialized in the native platform of the Cordova app.
   * For the Android platform:
      * Open the **[Cordova application root folder] → platforms → android → src → com → sample → [app-name] → MainActivity.java** file.
      * Look for the `onCreate` method and enable `LIFECYCLE` and `NETWORK` activities by following the steps:
         * To enable client lifecycle event logging, add the following line:
            ```Java
            WLAnalytics.addDeviceEventListener(DeviceEvent.LIFECYCLE);
            ```
            {: codeblock}
         * To enable client network-event logging, add the following line:
            ```Java
            WLAnalytics.addDeviceEventListener(DeviceEvent.NETWORK);
            ```
            {: codeblock}
      * Build the Cordova project by running the command: `cordova build`.
   * For the iOS platform:
      * Open the **[Cordova application root folder] → platforms → ios → Classes** folder and find the **AppDelegate.swift** (Swift) file.
      * To enable `LIFECYCLE` and `NETWORK` activities, do the following steps.
         * To enable client lifecycle event logging, add the following line:
            ```Swift
            WLAnalytics.sharedInstance().addDeviceEventListener(LIFECYCLE);
            ```
            {: codeblock}
         * To enable client network-event logging, add the following line:
            ```Swift
            WLAnalytics.sharedInstance().addDeviceEventListener(NETWORK);
            ```
            {: codeblock}
      * Build the Cordova project by running the command: `cordova build`.

1. You now initialized your application to collect analytics data. Next, you can send analytics data to Mobile Analytics.
   Use the following APIs to start recording and sending usage analytics:
   ```Javascript
   // Send recorded usage analytics to the Mobile Analytics

   WL.Analytics.send();
   ```
   {: codeblock}

1. To capture and send application logs to the {{site.data.keyword.mobileanalytics_short}} service, use the {{site.data.keyword.mobileanalytics_short}} Client SDK logger APIs.
   The {{site.data.keyword.mobileanalytics_short}} Client SDK logging [framework](#x2023472){: term} supports the following log levels, which are listed from least to most verbose, with suggested usage guidelines:
   * FATAL - Use for unrecoverable crashes or hangs. The FATAL level is reserved for logging unrecoverable errors, which appear to users as an application crash
   * ERROR - Use for unexpected exceptions or unexpected network protocol errors
   * WARN - Use to log usage warnings that aren’t considered critical errors, such as usage of deprecated APIs or slow network response
   * INFO - Use for reporting initialization events and other data that might be important, but not urgent
   * DEBUG - Use for reporting debug statements to help developers resolve application defects.
   When the logger level is set DEBUG, you also get {{site.data.keyword.mobileanalytics_short}} Client SDK logs, which are included when you send logs.
   * TRACE - used for method entry and exit points
   {: note}

   The following code snippets show sample Logger usage for Cordova:
   ```Javascript
   // Set the logging level (optional)
   // The default setting is DEBUG
   WL.Logger.config({"level": "INFO"});

   //Create a logger instance. You can create multiple loggers to organize your logs as you wish
   var logger = WL.Logger.create({ pkg: 'loggerName' });

   // Log messages with different levels
   // Debug message for feature 1
   // Info message for feature 2
   logger.debug("debug","debug message");
   //the logger.debug message is not logged because the logLevelFilter is set to Info
   logger.info("info","info message");

   // Send logs to the Mobile Analytics
   logger.send();
   ```
   {: codeblock}

1. To get insights on user onboarding patterns (new users versus returning users), you must associate a user identity with your application session. There is no specific API available from JavaScript level. But this can be done in the native code by calling the following API:

   **Android:**
      ```java
      WLAnalytics.setUserContext("userName or userIdentity");
      ```
      {: codeblock}

   **iOS:**
      ```Swift
      WLAnalytics.sharedInstance().setUserContext("userName or userIdentity")
      ```
      {: codeblock}

    All analytics data that is captured and stored locally is sent to the {{site.data.keyword.mobileanalytics_short}} service only when the WL.Analytics.send() API in JavaScript level [or] WLAnalytics.send() API in android native [or] WLAnalytics.sharedInstance().send() API in iOS native is called.

1. To get insights into your applications HTTP network interaction patterns such as HTTP APIs called, number of requests and average response times you must use the {{site.data.keyword.mobilefoundation_short}} Service Client SDK's WLResourceRequest class to make the HTTP calls. Although you initialized Analytics for the capture of Network events, the use of `WLResourceRequest` enables the {{site.data.keyword.mobileanalytics_short}} to hook into the network calls and capture the relevant data. Make your HTTP calls by using following code.
   ```Javascript
   var resourceRequest = new WLResourceRequest("url-path", WLResourceRequest.GET);
   resourceRequest.send().then(
     onSuccess: function(response) {
         resultText = "Successfully called the resource: " + response.responseText;
     },

     onFailure: function(response) {
         resultText = "Failed to call the resource:" + response.errorMsg;
     }
   );
   ```
   {: codeblock}

1. To define Custom Analytics and define your own analytics data over what is supported inherently in the Client SDK, you might use the custom logging API
   ```Javascript
   //create custom data as key value pair
   WL.Analytics.log({"FromPage" : 'LoginPage'});

   //Send the captured custom data and log to the Mobile Analytics service
   WL.Analytics.send();
   ```
   {: codeblock}

   The logged custom data can be plotted over custom charts you can define in the {{site.data.keyword.mobileanalytics_short}} console to derive custom insights.

1. Use In-App User Feedback to deepen your application performance analysis. You can enable your application **users and testers** to provide rich contextual feedback to the app owners. **App owners** get real-time feedback from its users on the application usage experience which **App owners** and **Developers** can further act on. This step brings in significant agility to application up-keep. Use the following API to switch your application to Interactive Feedback Mode in any action handler in your application, for example, when you handle the click of a button or the selection of a menu item.
   ```Javascript
   WL.Analytics.triggerFeedbackMode();
   ```
   {: codeblock}

## What to do next?
{: #next_steps_analytics_cordova}

Try a simple sample from [here](https://github.com/MobileFirst-Platform-Developer-Center/mfp-analytics-samples/tree/release80/cordova){: external}. In less than 5 minutes, you can run the sample application and get a feel of what the API does. You can also notice how analytics shows up as different insights on the Analytics console. 

{{site.data.keyword.mobilefoundation_short}} Analytics Service provides [REST](#x3220987){: term} APIs to help developers with importing (POST) and exporting (GET) analytics data.

For more Analytics tutorials, see {{site.data.keyword.mobilefoundation_short}} documentation [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/){: external}.
{: note}

You can also learn to do the following.

* [Configure offline storage](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-configure_offline_storage_cordova).
* [Send in-app feedback](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-sending_in_app_user_feedback_cordova).
* [Receive Push Notifications](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-receiving_push_notifications_in_cordova).