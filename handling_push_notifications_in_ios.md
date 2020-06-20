---

copyright:
  years: 2020
lastupdated: "2020-04-29"

keywords: push notifications, notifications, set up ios app for notification

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
{: #receiving_push_notifications_in_ios}

For iOS applications to be able to receive and display incoming push notifications the application must first be configured.
{: shortdesc}

Refer to the following sections to learn how to handle incoming push notifications in client applications:

## Handling Push Notifications in iOS
{: #handling_push_notifications_in_ios}

{{site.data.keyword.mobilefirst_notm}}-provided Notifications API can be used to register &amp; unregister devices, and subscribe &amp; unsubscribe to tags. In this tutorial, you learn how to handle push notification in iOS applications by using Swift.
{: shortdesc}

For information about Silent or Interactive notifications, see:

* [Silent Notifications](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-silent_notifications#silent_notifications)
* [Interactive Notifications](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-interactive_notifications#interactive_notifications)

### Prerequisites
{: #prereqs-ios}

* {{site.data.keyword.mfserver_short}} to run locally, or a remotely running {{site.data.keyword.mfserver_short}}.
* {{site.data.keyword.mfp_cli_long_notm}} installed on the developer workstation

### Notifications Configuration
{: #notifications-configuration_ios}

Create an Xcode project or use and existing one.
If the {{site.data.keyword.mobilefirst_notm}} Native iOS SDK is not already present in the project, follow the instructions in the [Adding the {{site.data.keyword.mobilefoundation_short}} SDK to iOS applications](/docs/mobilefoundation-sw/add_sdk_to_ios_app.html#add_sdk_to_ios_app) tutorial.

### Adding the Push SDK
{: #adding-the-push-sdk-ios}

1. Open the project's existing **podfile** and add the following lines:

   ```xml
   use_frameworks!

   platform :ios, 8.0
   target "Xcode-project-target" do
        pod 'IBMMobileFirstPlatformFoundation'
        pod 'IBMMobileFirstPlatformFoundationPush'
   end

   post_install do |installer|
        workDir = Dir.pwd

        installer.pods_project.targets.each do |target|
            debugXcconfigFilename = "#{workDir}/Pods/Target Support Files/#{target}/#{target}.debug.xcconfig"
            xcconfig = File.read(debugXcconfigFilename)
            newXcconfig = xcconfig.gsub(/HEADER_SEARCH_PATHS = .*/, "HEADER_SEARCH_PATHS = ")
            File.open(debugXcconfigFilename, "w") { |file| file << newXcconfig }

            releaseXcconfigFilename = "#{workDir}/Pods/Target Support Files/#{target}/#{target}.release.xcconfig"
            xcconfig = File.read(releaseXcconfigFilename)
            newXcconfig = xcconfig.gsub(/HEADER_SEARCH_PATHS = .*/, "HEADER_SEARCH_PATHS = ")
            File.open(releaseXcconfigFilename, "w") { |file| file << newXcconfig }
        end
   end
   ```
   {: codeblock}

   - Replace **Xcode-project-target** with the name of your Xcode project's target.

1. Save and close the **podfile**.
1. From a **Command-line** window, navigate into to the project's root folder.
1. Run the command `pod install`
1. Open project by using the **.xcworkspace** file.

### Notifications API
{: #notifications-api-ios}

#### MFPPush Instance
{: #mfppush-instance-ios}

All API calls must be called on an instance of `MFPPush`. To do this use `var` in a view controller such as `var push = MFPPush.sharedInstance();`, and then call `push.methodName()` throughout the view controller.

Alternatively, you can call `MFPPush.sharedInstance().methodName()` for each instance in which you need to access the push API methods.

### Challenge Handlers
{: #challenge-handlers-ios}

If the `push.mobileclient` scope is mapped to a **security check**, you need to make sure that matching **challenge handlers** exist and are registered before you use any of the Push APIs.

Learn more about challenge handlers in the [credential validation](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/authentication-and-security/credentials-validation/ios/){: external} tutorial.
{: note}

### Client-side
{: #client-side-ios}

| Swift Methods | Description  |
|---------------|--------------|
| [`initialize()`](#initialization) | Initializes MFPPush for supplied context. |
| [`isPushSupported()`](#is-push-supported) | Does the device support push notifications. |
| [`registerDevice(completionHandler: ((WLResponse!, NSError!) -> Void)!)`](#register-device--send-device-token) | Registers the device with the Push Notifications Service.|
| [`sendDeviceToken(deviceToken: NSData!)`](#register-device--send-device-token) | Sends the device token to the server |
| [`getTags(completionHandler: ((WLResponse!, NSError!) -> Void)!)`](#get-tags) | Retrieves one or more tags available in a push notification service instance. |
| [`subscribe(tagsArray: [AnyObject], completionHandler: ((WLResponse!, NSError!) -> Void)!)`](#subscribe) | Subscribes the device to the specified tags. |
| [`getSubscriptions(completionHandler: ((WLResponse!, NSError!) -> Void)!)`](#get-subscriptions)  | Retrieves all tags that the device is subscribed to. |
| [`unsubscribe(tagsArray: [AnyObject], completionHandler: ((WLResponse!, NSError!) -> Void)!)`](#unsubscribe) | Unsubscribes from a particular tag. |
| [`unregisterDevice(completionHandler: ((WLResponse!, NSError!) -> Void)!)`](#unregister) | Unregisters the device from the Push Notifications Service              |
{: caption="Table 2. Swift methods" caption-side="top"}

#### Initialization
{: #initialization-ios}

Initialization is required for the client application to connect to MFPPush service.

* The `initialize` method should be called first before you use any other MFPPush APIs.
* It registers the callback function to handle received push notifications.

```swift
MFPPush.sharedInstance().initialize();
```
{: codeblock}

#### Is push supported
{: #is-push-supported-ios}

Checks if the device supports push notifications.

```swift
let isPushSupported: Bool = MFPPush.sharedInstance().isPushSupported()

if isPushSupported {
    // Push is supported
} else {
    // Push is not supported
}
```
{: codeblock}

#### Register device &amp; send device token
{: #register-device-send-device-token-ios}

Register the device to the {{site.data.keyword.mobilepushshort}} service.

```swift
MFPPush.sharedInstance().registerDevice(nil) { (response, error) -> Void in
    if error == nil {
        self.enableButtons()
        self.showAlert("Registered successfully")
        print(response?.description ?? "")
    } else {
        self.showAlert("Registrations failed.  Error \(error?.localizedDescription)")
        print(error?.localizedDescription ?? "")
    }
}
```
{: codeblock}

<!--`options` = `[NSObject : AnyObject]` which is an optional parameter that is a dictionary of options to be passed with your register request, sends the device token to the server to register the device with its unique identifier.-->

```swift
MFPPush.sharedInstance().sendDeviceToken(deviceToken)
```
{: codeblock}

This API is typically called in the **AppDelegate** in the `didRegisterForRemoteNotificationsWithDeviceToken` method.
{: note}

#### Get tags
{: #get-tags-ios}

Retrieve all the available tags from the push notification service.

```swift
MFPPush.sharedInstance().getTags { (response, error) -> Void in
    if error == nil {
        print("The response is: \(response)")
        print("The response text is \(response?.responseText)")
        if response?.availableTags().isEmpty == true {
            self.tagsArray = []
            self.showAlert("There are no available tags")
        } else {
            self.tagsArray = response!.availableTags() as! [String]
            self.showAlert(String(describing: self.tagsArray))
            print("Tags response: \(response)")
        }
    } else {
        self.showAlert("Error \(error?.localizedDescription)")
        print("Error \(error?.localizedDescription)")
    }
}
```
{: codeblock}

#### Subscribe
{: #subscribe-ios}

Subscribe to desired tags.

```swift
var tagsArray: [String] = ["Tag 1", "Tag 2"]

MFPPush.sharedInstance().subscribe(self.tagsArray) { (response, error)  -> Void in
    if error == nil {
        self.showAlert("Subscribed successfully")
        print("Subscribed successfully response: \(response)")
    } else {
        self.showAlert("Failed to subscribe")
        print("Error \(error?.localizedDescription)")
    }
}
```
{: codeblock}

#### Get subscriptions
{: #get-subscriptions-ios}

Retrieve tags the device is subscribed to.

```swift
MFPPush.sharedInstance().getSubscriptions { (response, error) -> Void in
   if error == nil {
       var tags = [String]()
       let json = (response?.responseJSON)! as [AnyHashable: Any]
       let subscriptions = json["subscriptions"] as? [[String: AnyObject]]
       for tag in subscriptions! {
           if let tagName = tag["tagName"] as? String {
               print("tagName: \(tagName)")
               tags.append(tagName)
           }
       }
       self.showAlert(String(describing: tags))
   } else {
       self.showAlert("Error \(error?.localizedDescription)")
       print("Error \(error?.localizedDescription)")
   }
}
```
{: codeblock}

#### Unsubscribe
{: #unsubscribe-ios}

Unsubscribe from tags.

```swift
var tags: [String] = {"Tag 1", "Tag 2"};

// Unsubscribe from tags
MFPPush.sharedInstance().unsubscribe(self.tagsArray) { (response, error)  -> Void in
    if error == nil {
        self.showAlert("Unsubscribed successfully")
        print(String(describing: response?.description))
    } else {
        self.showAlert("Error \(error?.localizedDescription)")
        print("Error \(error?.localizedDescription)")
    }
}
```
{: codeblock}

#### Unregister
{: #unregister-ios}

Unregister the device from push notification service instance.

```swift
MFPPush.sharedInstance().unregisterDevice { (response, error)  -> Void in
   if error == nil {
       // Disable buttons
       self.disableButtons()
       self.showAlert("Unregistered successfully")
       print("Subscribed successfully response: \(response)")
   } else {
       self.showAlert("Error \(error?.localizedDescription)")
       print("Error \(error?.localizedDescription)")
   }
}
```
{: codeblock}

### Handling a push notification
{: #handling-a-push-notification-ios}

Push notifications are handled by the native iOS [framework](#x2023472){: term} directly. Depending on your application lifecycle, different methods are called by the iOS framework.

For example, if a simple notification is received while the application is running, **AppDelegate**'s `didReceiveRemoteNotification` is triggered:

```swift
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable: Any]) {
    print("Received Notification in didReceiveRemoteNotification \(userInfo)")
    // display the alert body
      if let notification = userInfo["aps"] as? NSDictionary,
        let alert = notification["alert"] as? NSDictionary,
        let body = alert["body"] as? String {
          showAlert(body)
        }
}
```
{: codeblock}

Learn more about handling notifications in iOS from the [Apple documentation](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1){: external}.
{: note}

## Next steps
{: #next-steps-ios-push}

* [Configure offline storage](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-configure_offline_storage_ios).
* [Add {{site.data.keyword.mobilefoundation_short}} Analytics](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-instrument_ios_app).
* [Send in-app feedback](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-sending_in_app_user_feedback_ios).

For more information about Push Notifications, see [here](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-push_notifications).
{: note}
