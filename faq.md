---

copyright:
  years: 2020
lastupdated: "2020-04-29"

keywords: mobile foundation faq, updates to mobile foundation, commonly asked questions, common questions, releases, updates, support model, interim fixes

subcollection:  mobilefoundation-sw

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tip: .tip}
{:support: data-reuse='support'}
{:important: .important}
{:note: .note}
{:download: .download}
{:java: .ph data-hd-programlang='java'}
{:ruby: .ph data-hd-programlang='ruby'}
{:c#: .ph data-hd-programlang='c#'}
{:objectc: .ph data-hd-programlang='Objective C'}
{:python: .ph data-hd-programlang='python'}
{:javascript: .ph data-hd-programlang='javascript'}
{:php: .ph data-hd-programlang='PHP'}
{:swift: .ph data-hd-programlang='swift'}
{:reactnative: .ph data-hd-programlang='React Native'}
{:csharp: .ph data-hd-programlang='csharp'}
{:ios: .ph data-hd-programlang='iOS'}
{:android: .ph data-hd-programlang='Android'}
{:cordova: .ph data-hd-programlang='Cordova'}
{:xml: .ph data-hd-programlang='xml'}
{:faq: data-hd-content-type='faq'}
{:external: target="_blank" .external}

# FAQs
{: #mfp-faq}

This FAQ provides answers to common questions about the {{site.data.keyword.mobilefoundation_long}} service.
{: shortdesc}

## What is the support policy for {{site.data.keyword.mobilefoundation_short}} 
{: #support-policy}
{: faq}
{: support}

IBM {{site.data.keyword.mobilefoundation_short}} v8.0 has a Continuous Delivery support policy.
To learn more about the continuous delivery support model, refer to the [Mobile Foundation v8.0 CD support announcement](https://www-01.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/0/897/ENUS217-390/index.html&request_locale=en).

## Where to get the information related to {{site.data.keyword.mobilefoundation_short}} iFixes and CD Updates?
{: #info_ifixes_cdupdates}
{: faq}
{: support}

You can find the information that is related to the list of all interim fixes and CD Updates that are released for Mobile Foundation v8.0 [here](https://mobilefirstplatform.ibmcloud.com/blog/2018/05/18/8-0-master-ifix-release/){: external}.

## What are the features released with {{site.data.keyword.mobilefoundation_short}} CD Updates?
{: #cd_features}
{: faq}
{: support}

You can view the list of features that are released in Mobile Foundation v8.0 CD Updates in the release notes [here](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-release_notes).

## Why is *Preinstall* disabled for {{site.data.keyword.mobilefoundation_short}}?
{: #preinstall_disabled}
{: faq}
{: support}

There are no tasks to be run before the actual installation of {{site.data.keyword.mobilefoundation_short}}, hence the *Preinstall* step is disabled. 

## Though Analytics Receiver component is enabled in the deployment values, the component is not installed. What is the reason?
{: #analyticsrcvr_not_installed}
{: faq}
{: support}

Analytics Receiver component is used by Mobile Analytics component, hence it is installed only if you enabled the deployment of Mobile Analytics component along with the Analytics Receiver component.

## Can I use the same Schematics workspace name during an update of {{site.data.keyword.mobilefoundation_short}}?
{: #schematics_wkspace_unique}
{: faq}
{: support}

Schematics workspace has to be unique for each installation plan. Since {{site.data.keyword.mobilefoundation_short}} update is also an installation action, you must provide a new unique name to the Schematics workspace during the update of {{site.data.keyword.mobilefoundation_short}}.

## When I install {{site.data.keyword.mobilefoundation_short}} I am required to provide the Persistent Volume Claim (PVC), will this also create the PVC?
{: #pvc_creation}
{: faq}
{: support}

Persistent Volume Claim is not created as part of the installation process. You need to ensure that the PVC exists before you can provide the PVC name in the deployment values section during the installation of {{site.data.keyword.mobilefoundation_short}}. Ensure that the PVC exists in the same namespace where you intend to deploy {{site.data.keyword.mobilefoundation_short}}.

## When I uninstall {{site.data.keyword.mobilefoundation_short}} the Persistent Volume Claim (PVC) is deleted, is this the expected behavior?
{: #pvc_deletion}
{: faq}
{: support}

The resources associated with {{site.data.keyword.mobilefoundation_short}} deployment gets removed when you uninstall {{site.data.keyword.mobilefoundation_short}}. Ensure you choose the right option when you choose to delete the associated Schematics workspace. Also, ensure to use the name of the StorageClass with *Retain policy* to persist the storage data. As a good practice, it is recommended that you make a note of the Persistent Volume (PV) that is created while specifying the name of the StorageClass, for the dynamic provisioning of the storage.


## What are the supported databases for {{site.data.keyword.mobilefoundation_short}}?
{: #db_supported}
{: faq}
{: support}

Currently, IBM Db2 is the only supported database.


