---

copyright:
  years: 2020
lastupdated: "2020-04-23"

keywords: Mobile Foundation SDK, web sdk, adding sdks to app, mobile app development, web application

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
{: #add_sdk_to_web_app}

## Adding the Web SDK to your app
{: #adding-web-sdk-to-your-app}
{: help}
{: support}

This SDK is the Core SDK for {{site.data.keyword.IBM_notm}} {{site.data.keyword.mobilefoundation_short}} consisting of APIs for implementing {{site.data.keyword.mobilefoundation_short}} security, authorization, logging, calling adapters and other core functions. Perform the following steps to add the Web SDK to your application.

## Step 1: Download the SDK

1. From a command-line window, navigate to your [web application’s](#x2116500){: term} root folder.

2. Run the following command.

   ```bash
   npm install ibm-mfp-web-sdk
   ```
   {: codeblock}

   This creates a directory with files such as `ibmmfpf.js`.

## Step 2: Referencing the SDK file in the web application.

1. You can reference the file `ibmmfpf.js` in the HEAD element.

   ```xml
  <head>
      ...
      ...
      <script type="text/javascript" src="node_modules/ibm-mfp-web-sdk/ibmmfpf.js"></script>
   </head>
   ```
   {: codeblock} 

2. Optionally, you can also use RequireJS library add the SDK.

   ```HTML
      <script type="text/javascript" src="node_modules/requirejs/require.js" data-main="index"></script>
   ```
   {: codeblock}

   ```JavaScript
      require.config({
      'paths': {
         'mfp': 'node_modules/ibm-mfp-web-sdk/ibmmfpf'
         }
      });

      require(['mfp'], function(WL) {
         // application logic.
      });
   ```
   {: codeblock}

5. Initialize the {{site.data.keyword.mobilefoundation_short}} web SDK by specifying the context root and application ID values in the main JavaScript file of your web application.
   ```javascript
   var wlInitOptions = {
      mfpContextRoot : '/mfp', // "mfp" is the default context root in the {{site.data.keyword.mobilefoundation_short}}
      applicationId : 'com.sample.mywebapp' // Replace with your own value.
      sessionMode : true //This is an optional paramter. Setting this to true ensures that MFP related data is stored in the session rather than in the local storage. If this option is set to false or not set at all, default is local storage.
   };

   WL.Client.init(wlInitOptions).then (
      function() {
         // Application logic.
   });
   ```
   {: codeblock}

   **mfpContextRoot** is the context root that is used by the {{site.data.keyword.mobilefoundation_short}} Server.
   **applicationId** is the application package name when you register the application.
   
## Next steps
{: #next-steps-web}

* [Add {{site.data.keyword.mobilefoundation_short}} Analytics](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-instrument_your_app_web).

For more Web tutorials, see {{site.data.keyword.mobilefoundation_short}} documentation [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/web-tutorials/){: external}.
{: note}
