---

copyright:
  years: 2020
lastupdated: "2020-04-29"

keywords: push notifications, notifications, set up windows app for notification

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

# Receive {{site.data.keyword.mobilepushshort}}
{: #receiving_push_notifications_in_windows}

For Windows&trade; applications to be able to receive and display incoming push notifications the application must first be configured.
{: shortdesc}
Microsoft, Windows, Windows NT, and the Windows logo are trademarks of Microsoft Corporation in the United States, other countries, or both.

## Handling Push Notifications in Windows 8.1 Universal and Windows 10 UWP
{: #handling_push_notifications_in_win}

{{ site.data.keyword.mobilefirst_notm }}-provided Notifications API can be used to register &amp; unregister devices, and subscribe &amp; unsubscribe to tags. In this tutorial, you learn how to handle push notification in native Windows 8.1 Universal and Windows 10 UWP applications by using C#.

### Prerequisites
{: #prereqs-windows}

* {{ site.data.keyword.mfserver_short_notm }} to run locally, or a remotely running {{ site.data.keyword.mfserver_short_notm }}.
* {{ site.data.keyword.mobilefirst_notm  }} [CLI](#x2008863){: term} installed on the developer workstation

### Notifications Configuration
{: #notifications-configuration-windows}

Create a Visual Studio project or use an existing one.  

If the {{ site.data.keyword.mobilefirst_notm }} Native Windows SDK is not already present in the project, follow the instructions in the [Adding the {{ site.data.keyword.mobilefirst_notm }} SDK to Windows applications](http://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/application-development/sdk/windows-8-10/) tutorial.

### Adding the Push SDK
{: #adding-the-push-sdk-windows}

1. Select Tools → NuGet Package Manager → Package Manager Console.
1. Choose the project where you want to install the {{ site.data.keyword.mobilefirst_notm }} Push component.
1. Add the {{ site.data.keyword.mobilefirst_notm }} Push SDK by running the **Install-Package IBM.MobileFirstPlatformFoundationPush** command.

### Pre-requisite WNS configuration
{: pre-requisite-wns-configuration}

1. Ensure that the application is with Toast notification capability. Enable it in `Package.appxmanifest`.
1. Ensure `Package Identity Name` and `Publisher` should be updated with the values that are registered with WNS.
1. (Optional) Delete TemporaryKey.pfx file.

### Notifications API
{: #notifications-api-windows}

#### MFPPush Instance
{: #mfppush-instance-windows}

All API calls must be called on an instance of `MFPPush`. Do this by creating a variable such as `private MFPPush PushClient = MFPPush.GetInstance();`, and then calling `PushClient.methodName()` throughout the class.

Alternatively you can call `MFPPush.GetInstance().methodName()` for each instance in which you need to access the push API methods.

#### Challenge Handlers
{: #challenge-handlers-windows}

If the `push.mobileclient` scope is mapped to a **security check**, you need to make sure that matching challenge handlers exist and are registered before you use any of the Push APIs.

Learn more about challenge handlers in the [credential validation ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/authentication-and-security/credentials-validation/windows-8-10/){: external} tutorial.
{: note}

### Client-side
{: #client-side-windows}

| C Sharp Methods          | Description          |
|--------------------------|----------------------|
| [`Initialize()`](#initialization-windows)                                                                            | Initializes MFPPush for supplied context.                               |
| [`IsPushSupported()`](#is-push-supported-windows)                                                                    | Does the device support push notifications.                             |
| [`RegisterDevice(JObject options)`](#register-device--send-device-token-windows)                  | Registers the device with the Push Notifications Service.               |
| [`GetTags()`](#get-tags-windows)                                | Retrieves the tags available in a push notification service instance. |
| [`Subscribe(String[] Tags)`](#subscribe-windows)     | Subscribes the device to one or more specified tags.                          |
| [`GetSubscriptions()`](#get-subscriptions-windows)              | Retrieves all tags that the device is subscribed to.               |
| [`Unsubscribe(String[] Tags)`](#unsubscribe-windows) | Unsubscribes from a particular tag.                                  |
| [`UnregisterDevice()`](#unregister-windows)                     | Unregisters the device from the Push Notifications Service              |
{: caption="Table 4. C Sharp methods" caption-side="top"}

#### Initialization
{: #initialization-windows}

Initialization is required for the client application to connect to MFPPush service.

* The `Initialize` method should be called first before you use any other MFPPush APIs.
* It registers the callback function to handle received push notifications.

```csharp
MFPPush.GetInstance().Initialize();
```
{: codeblock}

#### Is push supported
{: #is-push-supported-windows}

Checks if the device supports push notifications.

```csharp
Boolean isSupported = MFPPush.GetInstance().IsPushSupported();

if (isSupported ) {
    // Push is supported
} else {
    // Push is not supported
}
```
{: codeblock}

#### Register device &amp; send device token
{: #register-device-send-device-token-windows}

Register the device to the push notifications service.

```csharp
JObject Options = new JObject();
MFPPushMessageResponse Response = await MFPPush.GetInstance().RegisterDevice(Options);         
if (Response.Success == true)
{
    // Successfully registered
} else {
    // Registration failed with error
}
```
{: codeblock}

#### Get tags
{: #get-tags-windows}

Retrieve all the available tags from the push notification service.

```csharp
MFPPushMessageResponse Response = await MFPPush.GetInstance().GetTags();
if (Response.Success == true)
{
    Message = new MessageDialog("Avalibale Tags: " + Response.ResponseJSON["tagNames"]);
} else{
    Message = new MessageDialog("Failed to get Tags list");
}
```
{: codeblock}

#### Subscribe
{: #subscribe-windows}

Subscribe to desired tags.

```csharp
string[] Tags = ["Tag1" , "Tag2"];

// Get subscription tag
MFPPushMessageResponse Response = await MFPPush.GetInstance().Subscribe(Tags);
if (Response.Success == true)
{
    //successfully subscribed to push tag
}
else
{
    //failed to subscribe to push tags
}
```
{: codeblock}

#### Get subscriptions
{: #get-subscriptions-windows}

Retrieve tags the device is subscribed to.

```csharp
MFPPushMessageResponse Response = await MFPPush.GetInstance().GetSubscriptions();
if (Response.Success == true)
{
    Message = new MessageDialog("Avalibale Tags: " + Response.ResponseJSON["tagNames"]);
}
else
{
    Message = new MessageDialog("Failed to get subcription list...");
}
```
{: codeblock}

#### Unsubscribe
{: #unsubscribe-windows}

Unsubscribe from tags.

```csharp
string[] Tags = ["Tag1" , "Tag2"];

// unsubscribe tag
MFPPushMessageResponse Response = await MFPPush.GetInstance().Unsubscribe(Tags);
if (Response.Success == true)
{
    //succes
}
else
{
    //failed to subscribe to tags
}
```
{: codeblock}

#### Unregister
{: #unregister-windows}

Unregister the device from push notification service instance.

```csharp
MFPPushMessageResponse Response = await MFPPush.GetInstance().UnregisterDevice();         
if (Response.Success == true)
{
    // Successfully registered
} else {
    // Registration failed with error
}
```
{: codeblock}

### Handling a push notification
{: #receiving-a-push-notification-windows}

To handle a push notification, you need to set up a `MFPPushNotificationListener`. This can be achieved by implementing the following method.

1. Create a class by using interface of type MFPPushNotificationListener

   ```csharp
   internal class NotificationListner : MFPPushNotificationListener
   {
        public async void onReceive(String properties, String payload)
   {
        // Handle push notification here      
   }
   }
   ```
   {: codeblock}

1. Set the class to be the listener by calling `MFPPush.GetInstance().listen(new NotificationListner())`
1. In the onReceive method, you receive the push notification and can handle the notification for the desired behavior.

### Windows Universal Push Notifications Service
{: #windows-universal-push-notifications-service}

No specific port needs to be open in your server configuration.

WNS uses regular http or [HTTPS](#x2193603){: term} requests.

## Next steps
{: #next-steps-windows-push}

For more information about Push Notifications, see [here](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-push_notifications).
{: note}
