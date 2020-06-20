---

copyright:
  years: 2020
lastupdated: "2020-04-29"

keywords: mobile analytics, instrumenting Web app

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
{: #instrument_your_app_web}

{{site.data.keyword.mobileanalytics_short}} provides key application usage and application performance insights for mobile application developers and application owners.

You need to instrument your mobile application to use the {{site.data.keyword.mobileanalytics_short}} feature to monitor your application usage, performance and to get other statistics. 
Instrumenting you application has the following steps:

1. Import and install the Mobile Analytics Client SDK.
2. Instrument your application based on the type of analytics data you want to collect.

## Instrument your Web application
{: #instrument_web_app}

Steps to instrument your [Web application](#x2116500){: term}:

### Step 1: Import and install the {{site.data.keyword.mobileanalytics_short}} Client SDK for Web
{: #install_analytics_sdk_web }

#### Installing the Web Client SDK
{: #install_web_sdk}
Instrument your web application by using the {{site.data.keyword.mobileanalytics_short}} SDK.

1. Navigate to the root folder of your web application and run the following command. Add the SDK to your web application by using [npm](https://www.npmjs.com/package/ibm-mfp-web-sdk){: external}
   ```bash
   npm install ibm-mfp-web-sdk
   ```
   {: codeblock}

### Step 2: Instrument your Web application based on the type of analytics data you want to collect
{: #instrument_app_based_on_data_web }

1. Reference the ibmmfpf.js and ibmmfpfanalytics.js file in the `head` element of your main html page

   ```html
   <head>
     ....
     <script type="text/javascript" src="node_modules/ibm-mfp-web-sdk/ibmmfpf.js"></script>
     <script type="text/javascript" src="node_modules/ibm-mfp-web-sdk/lib/analytics/ibmmfpfanalytics.js"></script>
   </head>
   ```
   {: codeblock}
   {: web}

1. Initialize the {{site.data.keyword.mobilefoundation_short}} Web SDK by specifying the context root and application ID values in the main JavaScript file of your web application

   ```Javascript
   var wlInitOptions = {
     mfpContextRoot : '/mfp', // "mfp" is the default context root in the {{site.data.keyword.mobilefoundation_short}}
     applicationId : 'com.sample.mywebapp' // Replace with your own value.
   };

   WL.Client.init(wlInitOptions).then (
     function() {
       // Application logic.
     }
   );
   ```
   {: codeblock}

   Before you call any of the following analytic methods, you must ensure that your application embeds the required code to authenticate and authorize the device with the {{site.data.keyword.mobilefoundation_short}} service. This step is a common step that is required of all {{site.data.keyword.mobilefoundation_short}} services applications and is not specific to Analytics data capture. <!--  Refer <need to link doc that talks about auth> -->

   With initialization, complete your application is now enabled to capture device information and {{site.data.keyword.mobileanalytics_short}} SDK logs with no further code added. Any further APIs and code that is discussed in the following sections is optional and can be added based on what sort of analytics data you want to capture.

1. Add the following line to your application logic to capture application lifecycle events and network events.

   ```Javascript
   ibmmfpfanalytics.logger.config({analyticsCapture: true});
   ```
   {: codeblock}

1. You now initialized your application to capture analytics data. Next, you must send the captured data to the {{site.data.keyword.mobileanalytics_short}} service. Use the following API to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service.

   ```Javascript
   ibmmfpfanalytics.send();
   ```
   {: codeblock}

   You are free to decide when to call this API in your application flow to send the captured analytics data to the M{{site.data.keyword.mobileanalytics_short}} service. Until this sends, all captured analytics data is stored locally on the device.

1. To capture and send application logs to the {{site.data.keyword.mobileanalytics_short}} service, use the {{site.data.keyword.mobileanalytics_short}} Client SDK logger APIs.
   The {{site.data.keyword.mobileanalytics_short}} Client SDK logging framework supports the following log levels, which are listed from least to most verbose, with suggested usage guidelines:
   * FATAL - Use for unrecoverable crashes or hangs. The FATAL level is reserved for logging unrecoverable errors, which appear to users as an application crash
   * ERROR - Use for unexpected exceptions or unexpected network protocol errors
   * WARN - Use to log usage warnings that aren’t considered critical errors, such as usage of deprecated APIs or slow network response
   * INFO - Use for reporting initialization events and other data that might be important, but not urgent
   * DEBUG - Use for reporting debug statements to help developers resolve application defects.
      When the logger level is set DEBUG, you also get {{site.data.keyword.mobileanalytics_short}} Client SDK logs, which are included when you send logs.
   * TRACE - used for method entry and exit points
   {: note}

   The following code snippets show sample Logger usage for Web app:
   ```Javascript
   //Create a logger instance. You can create multiple loggers to organize your logs as you wish

   var logger = ibmmfpfanalytics.logger.pkg("loggerName");
   // Log messages with different levels
   // Debug message for feature 1
   // Info message for feature 2
   logger.debug("debug message");
   logger.info("info message");

   // Send logs to the Mobile Analytics
   ibmmfpfanalytics.send();
   ```
   {: codeblock}

   For the web SDK, the level cannot be set by the client. All logging is sent to the server until the configuration is changed by retrieving the server configuration profile.
   {: note}

1. To get insights on user onboarding patterns (new users versus returning users), you must associate a user identity with your application session. This can be done by calling the following API:
   ```Javascript
   ibmmfpfanalytics.setUserContext("userName or userIdentity");
   ```
   {: codeblock}

   All analytics data that is captured and stored locally is sent to the {{site.data.keyword.mobileanalytics_short}} service only when the ibmmfpfanalytics.send() API is called.

1. To get insights into your applications HTTP network interaction patterns such as HTTP APIs called, number of requests and average response times you must use the {{site.data.keyword.mobilefoundation_short}} Service Client SDK's WLResourceRequest class to make the HTTP calls. Although you initialized Analytics for the capture of Network events, the use of `WLResourceRequest` enables the {{site.data.keyword.mobileanalytics_short}} to hook into the network calls and capture the relevant data. Make your HTTP calls by using the following code.
   ```Javascript
   var resourceRequest = new WL.ResourceRequest("url_path", WLResourceRequest.GET);
   resourceRequest.send().then(function(response) {
         console.log('handle success' + JSON.stringify(data));
     },function(error){
         console.log('handle failure: ' + error);
     });
   ```
   {: codeblock}

1. To define Custom Analytics and define your own analytics data over what is supported inherently in the Client SDK, you might use the custom logging API:

   ```Javascript
   //custom data is sent with the addEvent method
   ibmmfpfanalytics.addEvent({'FromPage':'LoginPage'});

   //Send the captured custom data and log to the Mobile Analytics service
   ibmmfpfanalytics.send();
   ```
   {: codeblock}

   The logged custom data can be plotted over custom charts you can define in the Mobile Analytics console to derive custom insights.

## What to do next?
{: #next_steps_analytics_web}

Try a simple sample from [here](https://github.com/MobileFirst-Platform-Developer-Center/mfp-analytics-samples/tree/release80/web){: external}. In less than 5 minutes, you can run the sample application and get a feel of what the API does. You can also notice how analytics shows up as different insights on the Analytics console. 

{{site.data.keyword.mobilefoundation_short}} Analytics Service provides ReST APIs to help developers with importing (POST) and exporting (GET) analytics data.

For more Analytics tutorials, see {{site.data.keyword.mobilefoundation_short}} documentation [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/){: external}.
{: note}
