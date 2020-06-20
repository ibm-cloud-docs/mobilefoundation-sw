---

copyright:
  years: 2020
lastupdated: "2020-06-04"

keywords: uninstall, mobile foundation, license, deployment, uninstall, openshift, ocp cluster, red hat ocp cluster, mobile foundation software, application center, mobile foundation software, uninstall mobile foundation on IBM Cloud, unintall mobile foundation on openshift, mobile foundation on Red Hat OpenShift cluster, mobile foundation on RHOCP cluster

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

# Uninstall {{site.data.keyword.mobilefoundation_short}}
{: #uninstall-mf}

You can uninstall the {{site.data.keyword.mobilefoundation_short}} workspace or resources from the Schematics workspace for your {{site.data.keyword.mobilefoundation_short}} installation.

## Before you begin
{: #before-uninstall}
Ensure that you have the IBM Cloud [Identity and Access Management (IAM)](#x2193801){: term} permissions that are required for uninstallation. Refer to the [Before you begin](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-getting-started#before-you-begin) section of the Getting started page.

## Step 1. Use the Schematics workspace to view your installation of {{site.data.keyword.mobilefoundation_short}}

You can view your existing installation of {{site.data.keyword.mobilefoundation_short}} in two ways.

1. Log in to `cloud.ibm.com`.

2. From the menu, click **Schematics**.

3. Open the workspace with the installation of {{site.data.keyword.mobilefoundation_short}}.

Or.

1. Log in to `cloud.ibm.com`.

2. Click **Catalog**.

3. Under **Software**, search for {{site.data.keyword.mobilefoundation_short}} from the the list of offerings.

4. On the **Create** tab, expand **View the existing installations**.

5. Click the link to the Schematics workspace.

## Step 2. Delete resources and, optionally, the workspace

1. From the Schematics workspace for your {{site.data.keyword.mobilefoundation_short}} installation, click **Actions > Delete**.

2. In the **Delete workspace** dialog, select **Delete all associated resources** and, optionally, **Delete workspace**.

If you select to delete the workspace without also selecting to delete all associated resources, the resources remain on your cluster.
{: important}


## After uninstalling
{: #after-uninstall}

To view the logs, go to the **Activity** view from the menu, then click **View logs** on the uninstallation action.


