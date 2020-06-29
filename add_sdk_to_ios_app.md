---

copyright:
  years: 2020
lastupdated: "2020-04-23"

keywords: Mobile Foundation SDK, ios sdk, adding sdks to app, ios app development, native app, ios apps, swift app

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
{: #add_sdk_to_ios_app}

## Adding the iOS SDK to your app
{: #adding-ios-sdk-to-your-app}
{: help}
{: support}

This SDK is the Core SDK for {{site.data.keyword.IBM_notm}} {{site.data.keyword.mobilefoundation_short}} consisting of APIs for implementing {{site.data.keyword.mobilefoundation_short}} security, [authorization](#x2014653){: term}, logging, calling adapters and other core functions. Perform the following steps to add the iOS SDK to your application.

1. Go to root folder of your iOS app, run the following command to create a podfile.

   ```bash
   pod init
   ```
   {: codeblock}

2. Using your favorite code editor, open the `Podfile`.

   ```bash
   use_frameworks!
   platform :ios, 8.0
   target "ProjectName" do
       pod 'IBMMobileFirstPlatformFoundation'
   end
   ```
   {: codeblock}

3. Update pod by using the following command.

   ```bash
   pod update
   ```
   {: codeblock} 

4. Install pod by using the following command.

   ```bash
   pod install
   ```
   {: codeblock}

5. Open `[ProjectName].xcworkspace` to open the project in Xcode.

6. Add the `mfpclient.plist` file to Xcode workspace.

7. From a command prompt, navigate to the project folder and register your app with your {{site.data.keyword.mobilefoundation_short}} instance.

   ```bash
   mfpdev app register
   ```
   {: codeblock}
   
## Next steps
{: #next-steps-ios}

* [Configure offline storage](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-configure_offline_storage_ios).
* [Add {{site.data.keyword.mobilefoundation_short}} Analytics](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-instrument_ios_app).
* [Send in-app feedback](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-sending_in_app_user_feedback_ios).
* [Receive Push Notifications](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-receiving_push_notifications_in_ios).

For more iOS tutorials, see {{site.data.keyword.mobilefoundation_short}} documentation [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ios-tutorials/){: external}.
{: note}
