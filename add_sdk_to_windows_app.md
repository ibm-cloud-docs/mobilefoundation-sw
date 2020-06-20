---

copyright:
  years: 2020
lastupdated: "2020-04-29"

keywords: Mobile Foundation SDK, windows sdk, mobile app development, windows app, native app, windows 10 apps, NuGet tools, Windows application, UWP project

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
{: #add_sdk_to_windows_app}

## Adding the Client SDK to your Windows app
{: #adding-windows-sdk-to-your-app}
{: help
{: support}

This SDK is the Core SDK for {{site.data.keyword.IBM_notm}} {{site.data.keyword.mobilefoundation_short}} consisting of APIs for implementing {{site.data.keyword.mobilefoundation_short}} security, [authorization](#x2014653){: term}, logging, calling adapters and other core functions. 

<cite>Microsoft, Windows, Windows NT, and the Windows logo are trademarks of Microsoft Corporation in the United States, other countries, or both.</cite>

Add the client SDK to your Windows application by using the following steps.

1. Create a Windows 8.1 Universal or Windows 10 UWP project by using Visual Studio 2013/2015 or use an existing project.

2. To import {{site.data.keyword.mobilefoundation_short}} packages, use the NuGet package manager. NuGet is the package manager for the Microsoft development platform, including .NET. You can produce and use packages by using the NuGet client tools. The NuGet Gallery is the central package repository that is used by all package authors and users.

3. Open the Windows 8.1 Universal or Windows 10 UWP project in Visual studio 2013/2015. Right-click the project solution and select **Manage Nuget packages**.

4. In the search option, search for *IBM MobileFirst Platform*. Choose **IBM.MobileFirstPlatform.8.0.0.0**.

5. Click **Install**. This action installs the {{site.data.keyword.mobilefoundation_short}} Native SDK and its dependencies. This step also generates an empty `mfpclient.resw` file in the strings folder of the Visual Studio project.

6. Ensure that, at a minimum, the *Internet (Client)* capability is enabled in `Package.appxmanifest`.

## Manually adding the client SDK to your Windows app

You can prepare your environment for developing {{site.data.keyword.mobilefoundation_short}} applications by getting the [framework](#x2023472){: term} and library files manually. The {{site.data.keyword.mobilefoundation_short}} SDK for Windows 8 and Windows 10 Universal Windows Platform (UWP) is also available from NuGet.

1. Get the {{site.data.keyword.mobilefoundation_short}} SDK from the **Download Center → SDKs** tab on the {{site.data.keyword.mobilefoundation_short}} Operations Console.

2. Extract the contents of the downloaded SDK obtained in step 1.

3. Open the Windows Universal native project in Visual Studio. Perform the following steps.

  1. Select **Tools → NuGet Package Manager → Package Manager Settings**.

  2. Select **Package Sources** option. Click **+** icon to add new package source.

  3. Provide a name for the package source (for example: *windows8nuget*)

  4. Navigate to the MobileFirst SDK folder that was downloaded and extracted. Click **OK**.

  5. Click **Update** and then click **OK**.

  6. Right-click the **Solution project-name** in **Solution explorer** tab.

  7. Select **Manage NuGet Packages for Solutions → Online → windows8nuget**.

  8. Click **Install** option. You get the option to Select Projects.

  9. Ensure that all the check boxes are checked. Click **OK**.

## Next steps
{: #next-steps-windows}

* [Receive Push Notifications](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-receiving_push_notifications_in_windows).

For more Windows tutorials, see {{site.data.keyword.mobilefoundation_short}} documentation [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/windows-8-10-tutorials/){: external}.
{: note}

