---

copyright:
  years: 2020
lastupdated: "2020-04-29"

keywords: Mobile Foundation, Digital App Builder, DAB, low code app, mobile app builder, mobile app development, AI services, Watson services, drag and drop app builder 

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

# Overview
{: #digital_app_builder_overview}

## Key features

IBM Digital App Builder is a low-code tool, which helps to quickly create mobile, web and PWA (Progressive Web App) multi-channel applications with AI capabilities powered by Watson services. The apps that are created by using the Digital App Builder uses Mobile Foundation v8.0 for security, backend connectivity, and analytics.

The key features of Digital App Builder are as follows:

* Use this tool to quickly build digital apps that can run on multiple channels. With the Digital App Builder, you can drag-and-drop components to quickly build an app. This app can be targeted to multiple channels, like apps for iOS (iPhone, iPad), Android (Phone, Tabs), Progressive web apps (PWA), and web pages.

* Easily integrate Watson AI capabilities like Chatbot and Visual Recognition. Adding a chatbot or visual recognition capabilities to the app becomes as easy as adding a control. Also, easily train the AI service by adding a set of questions and answers or drag-and-drop a set of images to classify. There is no need for a data scientist to build a complex [machine learning model](#x7579194){: term}.

* Add data bound controls for microservice backends. A wizard can be used to import an Open API specification (Swagger) for a microservice. This helps to create a data set for building a front end for the service, which is bound to a data-bound UI control in the app. Switch to code view for doing advanced coding on the app.

* Add Push Notifications capability as part of Engagements.

* Use Live Update to dynamically toggle app features on or off after the app is live.

* Code the app by deploying mock [REST](#x3220987){: term} APIs to mimic an actual microservice in production.

* An app owner can enable Analytics for the app. The app sends data to the Mobile Foundation server.

* The app that is created uses open source technologies like Cordova, Ionic, or Angular. You can preview the app for various form factors before it is deployed. You can also use the quick start templates to build your apps (for example, Watson chatbot).

## Prerequisites and supported platforms

### Supported development platform:

* MacOS 10.13 (High Sierra or later)
* Windows 10
* Windows 10 Home
* Windows 10 Pro
* Windows 10 Enterprise

<cite>Microsoft, Windows, Windows NT, and the Windows logo are trademarks of Microsoft Corporation in the United States, other countries, or both.</cite>

### Software requirements (Prerequisites) for using the Digital App Builder:

*  Node Package Manager (npm) (Node.js 10.x)
*  Cordova 9.0.0
*  Ionic 4.12.0
*  CocoaPods (MacOS only)
*  Android Studio 2.x.x or later (To preview the app on Android emulator)
*  Mobile Foundation Server
      
### Prerequisites for running the app on device or emulator or simulator:

*  Android Studio (To preview the app on Android emulator)
*  For Installation instructions, see [here](https://developer.android.com/studio/){: external}.
*  For configuring an Android Virtual Machine. Follow the instructions [here](https://developer.android.com/studio/releases/emulator){: external}.
*  Android WebView version 68.X.XXXX.XX or later.
*  Chrome (To preview web platform)
*  Xcode (To preview the app on iOS simulator). For MacOS only, download and install Xcode from Apple App Store to preview the app.

### Other requirements

* [IBM Watson Assistant](https://cloud.ibm.com/catalog/services/watson-assistant) (for adding Chat service to the app)
* [IBM Watson Visual Recognition](https://cloud.ibm.com/developer/watson/starter-kits/watson-visual-recognition-basic) (for adding Visual recognition service to the app)

## Installing Digital App Builder

For detailed steps on installing Digital App Builder, see [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/digital-app-builder/installation/){: external}.

## Build your app

To start building your app by using Digital App Builder, follow the steps [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/digital-app-builder/getting-started/){: external}.
