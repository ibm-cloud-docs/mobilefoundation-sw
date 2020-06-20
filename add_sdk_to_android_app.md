---

copyright:
  years: 2020
lastupdated: "2020-04-23"

keywords: Mobile Foundation SDK, android sdk, adding sdks to app, android app development, mobile app development, android client sdk

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
{: #add_sdk_to_android_app}

## Adding the Android SDK to your app
{: #adding-android-sdk-to-your-app}
{: help
{: support}

This SDK is the Core SDK for {{site.data.keyword.IBM_notm}} {{site.data.keyword.mobilefoundation_short}} consisting of APIs for implementing {{site.data.keyword.mobilefoundation_short}} security, [authorization](#x2014653){: term}, logging, calling adapters and other core functions. Perform the following steps to add the Android SDK to your application.

1. Open Android Studio, choose the Android view and choose **Gradle Scripts**. Select the `build.gradle (Module: app)` file.

2. Add the following line to the `dependencies` section.

   ```bash
   compile 'com.ibm.mobile.foundation:ibmmobilefirstplatformfoundation:8.0.+'
   ```
   {: codeblock}

3. Add the following line to the `android` section.

   ```
   packagingOptions {
               pickFirst 'META-INF/ASL2.0'
               pickFirst 'META-INF/LICENSE'
               pickFirst 'META-INF/NOTICE'
      }
   ```
   {: codeblock}

4. In the Android view, open **app → manifests → AndroidManifest.xml** file. Add the following permissions before the `application` element.

   ```xml
   <uses-permission android:name="android.permission.INTERNET"/>
   <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
   ```
   {: codeblock}

5. Add the MobileFirst UI activity next to the existing `activity` element

   ```xml
   <activity android:name="com.worklight.wlclient.ui.UIActivity" />
   ```
   {: codeblock}

## Next steps
{: #next-steps-android}

* [Configure offline storage](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-configure_offline_storage_android).
* [Add {{site.data.keyword.mobilefoundation_short}} Analytics](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-instrument_your_app_android).
* [Send in-app feedback](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-sending_in_app_user_feedback_android).
* [Receive Push Notifications](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-receiving_push_notifications_in_android).

For more Android tutorials, see {{site.data.keyword.mobilefoundation_short}} documentation [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/android-tutorials/){: external}.
{: note}
