---

copyright:
  years: 2020
lastupdated: "2020-05-06"

keywords: mobile analytics, send in-app user feedback cordova app

subcollection:  mobilefoundation-sw

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:external: target="_blank" .external}

# Capture and send in-app user feedback
{: #sending_in_app_user_feedback_cordova}

In-App User Feedback deepens your application performance analysis. You can enable your application users and testers to provide rich contextual feedback to the app owners. App owners get real-time feedback from its users on the application usage experience, which App owners and Developers can further act on. This feature brings in significant agility to application up-keep. Use the following API to switch your application to Interactive Feedback Mode in any action handler in your application, for example, when you handle the click of a button or the selection of a menu item.

To enable your Cordova app to send in-app user feedback, perform the following steps.

1. Add the following plug-in to include In-App Feedback capability into your Cordova application and ensure that the plug-in is successfully added.

   ```bash
   cordova plugin add cordova-plugin-mfp-analytics
   ```
   {: codeblock}

2. Use the following JavaScript API method in the action handler of your Cordova application.

   ```javascript
   WL.Analytics.triggerFeedbackMode();
   ```
   {: codeblock}

## Next steps
{: #next-steps-cordova-feedback}

* [Configure offline storage](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-configure_offline_storage_cordova).
* [Add {{site.data.keyword.mobilefoundation_short}} Analytics](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-instrument_your_app_cordova).
* [Receive Push Notifications](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-receiving_push_notifications_in_cordova).

For more information about in-app feedback, see {{site.data.keyword.mobilefoundation_short}} documentation [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/console/userfeedback/){: external}.
{: note}
