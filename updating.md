---

copyright:
  years: 2020
lastupdated: "2020-06-04"

keywords: updating, mobile foundation, license, deployment, update, openshift, ocp cluster, red hat ocp cluster, mobile foundation software, application center, mobile foundation software, update mobile foundation on IBM Cloud, update mobile foundation on openshift, mobile foundation on Red Hat OpenShift cluster, mobile foundation on RHOCP cluster

subcollection:  mobilefoundation-sw

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:term: .term}
{:important: .important}
{:tip: .tip}
{:note: .note}
{:external: target="_blank" .external}

# Update an existing {{site.data.keyword.mobilefoundation_short}} deployment
{: #update-mf}

You can update the existing deployment by adding or removing components. You can also update your deployment by making changes to the number of replicas.

## Before you begin
{: #before-update}
Ensure that you have the IBM Cloud [Identity and Access Management (IAM)](#x2193801){: term} permissions that are required for performing the udpate. Refer to the [Before you begin](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-getting-started#before-you-begin) section of the Getting started page.

## Updating {{site.data.keyword.mobilefoundation_short}}

Perform the following steps to update your {{site.data.keyword.mobilefoundation_short}} deployment.

1. Log in to `cloud.ibm.com`.

2. Click **Catalog**.

3. Under **Software**, search for {{site.data.keyword.mobilefoundation_short}} from the the list of offerings.

4. On the **Create** tab, expand the deployment values section and make the required changes.

5. Click **Install**. 

## After update
{: #after-update}

To view the logs, go to the **Activity** view from the menu, then click **View logs** on the update action.
After the update completes, verify that you can access the {{site.data.keyword.mobilefoundation_short}} dashboard of the updated deployment.
