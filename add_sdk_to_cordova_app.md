---

copyright:
  years: 2020
lastupdated: "2020-04-23"

keywords: Mobile Foundation SDK, cordova sdk, adding sdks to app, mobile app development cordova, hybrid mobile app, cordova client sdk

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
{: #add_sdk_to_cordova_app}

## Adding the Cordova SDK to your app
{: #adding-cordova-sdk-to-your-app}
{: help
{: support}

This SDK is the Core SDK for {{site.data.keyword.IBM_notm}} {{site.data.keyword.mobilefoundation_short}} consisting of APIs for implementing {{site.data.keyword.mobilefoundation_short}} security, [authorization](#x2014653){: term}, logging, calling adapters and other core functions. Perform the following steps to add the Cordova SDK to your application.

1. Create a Cordova project.

   ```bash
   cordova create Hello com.example.helloworld HelloWorld
   ```
   {: codeblock}

2. Perform change directory to the root of the Cordova project.

   ```bash
   cd Hello
   ```
   {: codeblock}

3. Add one or more supported platforms to the Cordova project by using the Cordova CLI.

   ```bash
   cordova platform add ios|android|windows
   ```
   {: codeblock}

4. Add the {{site.data.keyword.mobilefoundation_short}} core Cordova plug-in.

   ```bash
   cordova plugin add cordova-plugin-mfp
   ```
   {: codeblock}

5. Prepare the application resources by running the following command.

   ```bash
   cordova prepare
   ```
   {: codeblock}

6. Register the application to {{site.data.keyword.mobilefoundation_short}} server.

   ```bash
   mfpdev app register
   ```
   {: codeblock}
   
## Next steps
{: #next-steps-cordova}

* [Configure offline storage](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-configure_offline_storage_cordova).
* [Add {{site.data.keyword.mobilefoundation_short}} Analytics](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-instrument_your_app_cordova).
* [Send in-app feedback](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-sending_in_app_user_feedback_cordova).
* [Receive Push Notifications](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-receiving_push_notifications_in_cordova).

For more Cordova tutorials, see {{site.data.keyword.mobilefoundation_short}} documentation [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/cordova-tutorials/){: external}.
{: note}
