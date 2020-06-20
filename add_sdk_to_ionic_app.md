---

copyright:
  years: 2020
lastupdated: "2020-04-23"

keywords: Mobile Foundation SDK, ionic sdk, adding sdks to app, ionic client sdk, ionic project, ionic application template, ionic framework, hybrid app development, ionic cordova  

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
{: #add_sdk_to_ionic_app}

## Adding the Ionic SDK to your app
{: #adding-ionic-sdk-to-your-app}
{: help
{: support}

This SDK is the Core SDK for {{site.data.keyword.IBM_notm}} {{site.data.keyword.mobilefoundation_short}} consisting of APIs for implementing {{site.data.keyword.mobilefoundation_short}} security, [authorization](#x2014653){: term}, logging, calling adapters and other core functions. Perform the following steps to add the Ionic SDK to your application. Consider creating a project by using the {{site.data.keyword.mobilefoundation_short}} Ionic application template. The [template](#x2041200){: term} adds the necessary {{site.data.keyword.mobilefoundation_short}} specific plug-in entries to the Ionic project’s `config.xml` file and provides a {{site.data.keyword.mobilefoundation_short}} specific, ready-to-use, `index.js` file.

1. Create an Ionic project.

   ```bash
   ionic start `projectName` `starter-template`
   ```
   {: codeblock}


2. Perform change directory to the root of the Ionic project.

   ```bash
   cd `project-folder`
   ```
   {: codeblock}

   If you have an existing project, then navigate to the root of your existing Ionic project and add the {{site.data.keyword.mobilefoundation_short}} core Ionic Cordova plug-in.
   {: note}

3. Add the MobileFirst plug-ins by using the Ionic [CLI](#x2008863){: term} command.

   ```bash
   ionic cordova plugin add cordova-plugin-mfp
   ```
   {: codeblock}

4. Add one or more supported platforms to the Cordova project by using the Ionic CLI command.

   ```bash
   ionic cordova platform add {`ios|android|windows|browser`}
   ```
   {: codeblock}

5. Prepare the application resources by running the following command.

   ```bash
   ionic cordova prepare
   ```
   {: codeblock}

## Next steps
{: #next-steps-ionic}

* [Configure offline storage](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-configure_offline_storage_ionic).

For more Ionic tutorials, see {{site.data.keyword.mobilefoundation_short}} documentation [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ionic-tutorials/){: external}.
{: note}

