---

copyright:
  years: 2020
lastupdated: "2020-04-23"

keywords: Mobile Foundation SDK, reactnative sdk, adding sdks to app, application development, react native app, mobile app development, cross platform app development

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
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Add Client SDK
{: #add_sdk_to_reactnative_app}

## Adding the React Native SDK to your app
{: #adding-reactnative-sdk-to-your-app}
{: help}
{: support}

This SDK is the Core SDK for {{site.data.keyword.IBM_notm}} {{site.data.keyword.mobilefoundation_short}} consisting of APIs for implementing {{site.data.keyword.mobilefoundation_short}} security, authorization, logging, calling adapters and other core functions. To add {{site.data.keyword.mobilefoundation_short}} capabilities to an existing React Native app, you need to add the `react-native-ibm-mobilefirst` plug-in to your app. The `react-native-ibm-mobilefirst` plug-in contains {{site.data.keyword.mobilefoundation_short}} SDK. Perform the following steps to add the React Native plug-in to your React Native application.

1. Add this plug-in in the same way that you add any other `npm` plug-in to your app.

   ```bash
   npm install react-native-ibm-mobilefirst --save
   ```
   {: codeblock}

2. Create a React Native project, for example, *MobileFirstApp*. Use the React Native [CLI](#x2008863){: term} to create a new project.

   ```bash
   react-native init MobileFirstApp
   ```
   {: codeblock}

3. Now add the react native plug-in to your app.

   ```bash
   cd MobileFirstApp
   npm install react-native-ibm-mobilefirst --save
   ```
   {: codeblock}

4. Link your project so that all native dependencies are added to your React Native project.

   ```bash
   react-native link
   ```
   {: codeblock}

5. For Android, make the following changes to `AndroidManifest.xml` (`<PROJECT_ROOT>/android/app/src/main/`).

   ```xml
   <manifest
          xmlns:android="http://schemas.android.com/apk/res/android"
          xmlns:tools="http://schemas.android.com/tools"
          package="com.mobilefirstapp">
   ```
   {: codeblock}

6. Add **tools:replace='android:allowBackup'** to the `application` tag.

   ```xml
   <application
            android:name=".MainApplication"
            android:label="@string/app_name"
            android:icon="@mipmap/ic_launcher"
            android:allowBackup="false"
            android:theme="@style/AppTheme"
            tools:replace="android:allowBackup">
   ```
   {: codeblock}

7. For iOS, open Xcode, in the project navigator, drag and drop `mfpclient.plist` from `ios` folder. This step is applicable only for iOS platform.
   

## Next steps
{: #next-steps-reactnative}

* [Configure offline storage](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-configure_offline_storage_reactnative).

For more React Native tutorials, see {{site.data.keyword.mobilefoundation_short}} documentation [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/reactnative-tutorials/){: external}.
{: note}
