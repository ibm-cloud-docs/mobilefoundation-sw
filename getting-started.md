---

copyright:
  years: 2020
lastupdated: "2020-06-04"

keywords: getting started, mobile foundation, license, deployment, install, openshift, ocp cluster, red hat ocp cluster, mobile foundation software, application center, mobile app development, getting started with mobile app development, mobile app development on cloud, mobile app development platform, mobile backend services, mobile foundation software, mobile applications, install mobile foundation on IBM Cloud, intall mobile foundation on openshift, mobile foundation on Red Hat OpenShift cluster, mobile foundation on RHOCP cluster

subcollection:  mobilefoundation-sw

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:external: target="_blank" .external}

# Getting started with IBM {{site.data.keyword.mobilefoundation_short}}
{: #getting-started}

IBM {{site.data.keyword.mobilefoundation_short}} on [IBM Cloud](#x7301758){: term} is an integrated platform that helps you extend your business to mobile devices. {{site.data.keyword.mobilefoundation_short}} includes a comprehensive development environment, mobile-optimized [runtime](#x2391929){: term} middleware, a private enterprise application store, and an integrated management and analytics console. With {{site.data.keyword.mobilefoundation_short}}, developers can efficiently develop, connect, run, and manage rich mobile applications (apps) that accesses the capabilities of target mobile devices. {{site.data.keyword.mobilefoundation_short}} helps reduce time-to-market, cost, complexity of development, and provides a seamless client user experience across touch points.
{:shortdesc}

## What's in {{site.data.keyword.mobilefoundation_short}}

{{site.data.keyword.mobilefoundation_short}} includes the following components.

### {{site.data.keyword.mobilefoundation_short}} Server
The MobileFirst Server provides secure backend connectivity, application management, push notification support, analytics capabilities, and monitoring for {{site.data.keyword.mobilefoundation_short}} applications. For more information about {{site.data.keyword.mobilefoundation_short}} Server, see the [documentation](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/product-overview/components/server/){: external}.

### Push Notifications
{{site.data.keyword.mobilefoundation_short}} provides a unified set of API methods to send either push or SMS notifications to iOS, Android, Windows 8.1 Universal, Windows 10 UWP, and Cordova (iOS, Android) applications. Microsoft, Windows, Windows NT, and the Windows logo are trademarks of Microsoft Corporation in the United States, other countries, or both. The notifications are sent from the {{site.data.keyword.mobilefoundation_short}} Server to the vendor (Apple, Google, Microsoft, SMS Gateways) infrastructure, and from there to the relevant devices. For more information about Push Notifications, see the [documentation](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/notifications/){: external}.

<cite>Microsoft, Windows, Windows NT, and the Windows logo are trademarks of Microsoft Corporation in the United States, other countries, or both.</cite>

### {{site.data.keyword.mobilefoundation_short}} Analytics
To keep your user engagement relevant and effective you must gain insights into how your application is performing with users. {{site.data.keyword.mobilefoundation_short}} Analytics provides this feature with in-built visualizations (charts and tables). With minimal instrumentation of your application, you can readily visualize actionable insights on the {{site.data.keyword.mobilefoundation_short}} Analytics console. For more information about {{site.data.keyword.mobilefoundation_short}} Analytics, see the [documentation](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/){: external}.

### Live Update
Live Update feature in {{site.data.keyword.mobilefoundation_short}} provides a simple way to define and serve different configurations for users of an application. It includes a component in the {{site.data.keyword.mobilefoundation_short}} console for defining the structure and values of the configuration. A client SDK (available for Android and iOS native and for Cordova applications) is provided for consuming the configuration. For more information about Live Update, see the [documentation](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/application-development/live-update-service/){: external}.

### {{site.data.keyword.mobilefoundation_short}} Application Center
You can use the Application Center as an enterprise application store. With the Application Center, you can target some mobile applications to particular groups of users within the company. For more information about {{site.data.keyword.mobilefoundation_short}} Application Center, see the [documentation](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/appcenter/){: external}.

### {{site.data.keyword.mobilefoundation_short}} Client SDKs
{{site.data.keyword.mobilefoundation_short}} provides client-side SDKs that embed server functions within the target environment of deployed apps. These runtime client APIs are libraries that are integrated into the locally stored app code. You need to use them to add {{site.data.keyword.mobilefoundation_short}} features to your client apps. For more information about {{site.data.keyword.mobilefoundation_short}} Client SDKs, see the [documentation](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/application-development/sdk/){: external}.

### {{site.data.keyword.mobilefoundation_short}} Operations console
{{site.data.keyword.mobilefoundation_short}} Operations Console is used for the control and management of mobile applications. The {{site.data.keyword.mobilefoundation_short}} Operations console is also an entry point to learn about {{site.data.keyword.mobilefoundation_short}} development. From the console, you can download code examples, tools, and SDKs. For more information about {{site.data.keyword.mobilefoundation_short}} Operations console, see the [documentation](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/product-overview/components/console/){: external}.

### {{site.data.keyword.mobilefoundation_short}} CLI
You can use the {{site.data.keyword.mobilefoundation_short}} command-line interface (CLI) to develop and manage applications, in addition to using the {{site.data.keyword.mobilefoundation_short}} Operations Console. For more information about {{site.data.keyword.mobilefoundation_short}} CLI, see the [documentation](/docs/mobilefoundation-sw/mobilefoundation-sw-using_cli?topic=mobilefoundation-sw-mobile_foundation_cli).

## Before you begin
Before you install the {{site.data.keyword.mobilefoundation_short}}, you must set up a Red Hat OpenShift cluster. Go to [Red Hat OpenShift cluster](https://cloud.ibm.com/kubernetes/catalog/openshiftcluster) to create a cluster.

You must buy a license through [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/index.html). Following are the part numbers for IBM {{site.data.keyword.mobilefoundation_short}}. You can have one installation of IBM {{site.data.keyword.mobilefoundation_short}} per license.

| Part Number | Description |
|-------------|-------------|
| D24Q0LL |	IBM {{site.data.keyword.mobilefoundation_short}} Virtual Processor Core License + SW Subscription & Support 12 months |
| D24Q5LL | IBM {{site.data.keyword.mobilefoundation_short}} Virtual Processor Core Monthly License |
| E0Q8ZLL | IBM {{site.data.keyword.mobilefoundation_short}} Virtual Processor Core Annual SW Subscription & Support renewal 12 months |
| D24Q1LL | IBM {{site.data.keyword.mobilefoundation_short}} Virtual Processor Core SW Subscription & Support Reinstatement 12 months |

Make sure that your cluster meets the minimum scheduling capacity. It is recommended to install {{site.data.keyword.mobilefoundation_short}} components with 3 replicas each.

Elasticsearch is required if you install Analytics. Database (Db2) is required for all other {{site.data.keyword.mobilefoundation_short}} components.
By default, all components are enabled for install. To selectively install components, modify the deployment values during install.
{: note}

| Components | Memory (GB) | CPU (cores) | Disk (GB) | Nodes |
|------------|--------|-------------|-----------|-------|
| Database initialization job (Mandatory) | 0.3 | 0.3 | - | 1 |
| Server (Mandatory) | 2 | 1 | - | 3 |
| Analytics (Optional) | 2 | 1 | - | 3 |
| Analytics Receiver (Mandatory if Analytics is installed) | 1 | 0.75 | - | 3 |
| Live Update (Optional)| 1 | 0.75 | - | 3 |
| Push Notifications (Optional) | 2 | 1 | - | 3 |
| Application Center (Optional) | 2 | 1 | - | 3 |
| Elasticsearch (Mandatory if Analytics is installed) | 2 | 1 | - | 3 |
| Mobile Foundation Operator | 0.5 | 0.4 | - | 3 |
| Elasticsearch Operator | 0.5 | 0.4 | - | 3 |
| **Total** | ~13.5 | 7.6 | 5 | 3 |

Also, ensure that you have the correct IBM Cloud [Identity and Access Management (IAM)](#x2193801){: term} permissions.

| Service or Resource | IAM Roles |
|---------------------|-----------|
| 'Kubernetes Cluster' service | Manager and Writer |
| Resource Group containing the OCP cluster | Viewer |
| 'License and Entitlement' service | Editor |
| Schematics service | Manager |

For more information on IAM roles and permissions, see [Managing identity and access](/docs/iam?topic=iam-userroles).

## Step 1. Assign a license

On the {{site.data.keyword.mobilefoundation_short}} **Create** tab in the IBM Cloud catalog, assign a license.

The license that is bought through IBM Passport Advantage appears in the list of available entitlements. Click an entitlement block to select it. Click **Assign**.

## Step 2. Configure your installation environment

Select a target Red Hat OpenShift cluster, and then select or type a project name in the **Project** field.

## Step 3. Configure your workspace

In this step, define how your installation is managed in a Schematics workspace.

You can type a name for the installation in the **Name** field, or use the default. To view your existing resources, see the [resource list page](https://cloud.ibm.com/resources).

Select a resource group from the Resource group list, or use the default. For more information on resource groups, see [Best practices for organizing resources in a resource group](/docs/resources?topic=resources-bp_resourcegroups#bp_resourcegroups).

Enter any tags that you want to use to organize this resource in the **Tags** field in a comma-separated list. Tags can contain special characters, which can be used in creating key-value pairs such as key:value for grouping related tags. Tags are visible across the account.

## Step 4. Run the pre-installation script

There is no preinstallation script to be executed. You can proceed to the following step.
{: note}

## Step 5. Set the deployment values

In the **Parameters without default values** section, provide the database related parameter values.

You can also create or connect to an existing [Db2 service on IBM Cloud](https://cloud.ibm.com/catalog/services/db2) (**Lite** plan not supported). Get the service credentials and use it to populate the database deployment values. 
{: note}

Expand **Parameters with default values** and change the parameter values as needed. 

For a list of deployment values for {{site.data.keyword.mobilefoundation_short}}, see [here](/docs/mobilefoundation-sw/mobilefoundation-sw-deployment-values?topic=mobilefoundation-sw-deployment-values).
{: tip}

## Step 6. Install {{site.data.keyword.mobilefoundation_short}}

Ensure that an entitlement is assigned. If not, you must get an entitlement.

Confirm your agreement to the license agreement by checking the checkbox. Then, click **Install**.

## Next steps
{: #next-steps-getting-started}

After the installation completes, verify that you can access the {{site.data.keyword.mobilefoundation_short}} dashboard.

1. Click the workspace name: **Schematics / Workspace /** *workspace_name*.

2. Click **View log** in the **Applying plan** activity.

3. After the **Applying plan** activity completes, you will see the *resource_controller_url* logged, copy its value.

4. Open a browser and paste the copied *resource_controller_url* value to the URL and hit **Enter**. This launches the {{site.data.keyword.mobilefoundation_short}} Operations console.

    On the workspace activity page, you can click **Offering dashboard** to launch the {{site.data.keyword.mobilefoundation_short}} Operations console.
    {: tip}

5. Get started with {{site.data.keyword.mobilefoundation_short}} by following the **How To** section of this documentation.

    For detailed documentation on {{site.data.keyword.mobilefoundation_short}}, see [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/all-tutorials/){: external}.
    {: note}




