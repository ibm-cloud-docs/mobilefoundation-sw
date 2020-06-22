---

copyright:
  years: 2020
lastupdated: "2020-06-22"

keywords: troubleshooting techniques, troubleshooting mobile foundation

subcollection:  mobilefoundation-sw

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:support: data-reuse='support'}
{:pre: .pre}
{:term: .term}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tip: .tip}
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
{:external: target="_blank" .external}

# Troubleshooting
{: #mf-troubleshooting}

To isolate and resolve problems with your {{site.data.keyword.IBM_notm}} products, you can use the troubleshooting information. This information contains instructions for using the problem-determination resources that are provided with your {{site.data.keyword.IBM_notm}} products, including {{site.data.keyword.mobilefoundation_short}}.
{: shortdesc}

## {{site.data.keyword.mobilefoundation_short}} deployment fails applying custom resource yaml for the component
{: #mf-software-deploy-fails-cr}
{: troubleshoot}
{: support}

{{site.data.keyword.mobilefoundation_short}} deployment failed with the error - 
*Error from server (MethodNotAllowed): error when creating "./ibm-mobilefoundation/inventory/ibmcloudEnablement/files/components/mf/deploy/crds/charts_v1_mfoperator_cr.yaml": create not allowed while custom resource definition is terminating
Failed to apply custom CR for the component - mf*
{: tsSymptoms}

Previous installation custom resource (CR) is in terminating state. 
{: tsCauses}

Ensure that the pre-existing deployments are uninstalled.
{: tsResolve}
	 
## Setting `db_type` to other database providers like Oracle or MySQL does not work
{: #mf-software-deploy-fails-db-error}
{: troubleshoot}
{: support}

Setting `db_type` to other databases like Oracle or MySQL does not work. Installation fails.
{: tsSymptoms}

Currently, the deployment supports IBM Db2 only. 
{: tsCauses}

Ensure the `db_type` is set to **DB2** in the deployment values section.
{: tsResolve}

## {{site.data.keyword.mobilefoundation_short}} deployment fails without creating any pods
{: #mf-software-deploy-fails-pods-not-created}
{: troubleshoot}
{: support}

{{site.data.keyword.mobilefoundation_short}} deployment failed and no pods created.
{: tsSymptoms}
	
Root cause might be various.
{: tsCauses}
	
1. Log in to the namespace of the OpenShift Container Platform (OCP) cluster by using a terminal. 
2. Check the operator pod logs by using the command `oc logs -f <operator-pod-name>`
{: tsResolve}

## {{site.data.keyword.mobilefoundation_short}} routes are not accessible
{: #mf-software-deploy-routes-not-accessible}
{: troubleshoot}
{: support}

{{site.data.keyword.mobilefoundation_short}} deployment successful, but routes are not accessible.
{: tsSymptoms}
	
Pods might be terminated.
{: tsCauses}
	
1. Log in to the namespace of the OpenShift Container Platform (OCP) cluster by using a terminal. 
2. Check the pod logs by using the commands `oc logs -f <operator-podname>` and `oc logs -f <failed-podname-if-exists>`. 
3. Also, check whether the machine has enough resources for the pods to run.
{: tsResolve}

## *push* or *liveupdate* components not deployed
{: #mf-software-install-components-not-deployed}
{: troubleshoot}
{: support}

Enabled *push* or *liveupdate* component but deployment fails.
{: tsSymptoms}
	
The deployment value `mfpserver_enabled` might be set to `false`.
{: tsCauses}

Ensure that server is enabled too.
{: tsResolve}
	
##  {{site.data.keyword.mobilefoundation_short}} deployment fails connecting to database
{: #mf-software-install-not-connecting-to-db}
{: troubleshoot}
{: support}

Deployment exits with a test database connection failure.
{: tsSymptoms}
	
Database details might be incorrect.
{: tsCauses}
	
Ensure that the database is reachable from a simple database client utility.
{: tsResolve}  

##  Uninstallation of {{site.data.keyword.mobilefoundation_short}} hangs
{: #mf-software-install-not-connecting-to-db}
{: troubleshoot}
{: support}

Uninstallation of {{site.data.keyword.mobilefoundation_short}} hangs indefinitely and the associated resources are not removed.
{: tsSymptoms}
	
This issue occurs because the CustomResourceDefinition (CRD) is stuck and needs to be cleared manually.
{: tsCauses}
	
1. From the terminal log in to the cluster using `oc` OpenShift CLI and run the following command.
	```bash
   oc patch crd/mfoperators.mf.ibm.com -p '{"metadata":{"finalizers":[]}}' --type=merge
  ```
  {: codeblock}
2. If applying the patch did not clear the resources, perform the following steps.
    * Execute the command `oc edit mfoperator.ibm.com`.
	  * Locate the keyword *finalizers* and delete the `uninstall*` line below the *finalizers* keyword and save the document.
	  * Ensure that the resources are cleaned up by running the `oc get pods` command.
{: tsResolve}  

## Techniques for troubleshooting problems
{: #ts_overview}

*Troubleshooting* is a systematic approach to solving a problem. The goal of troubleshooting is to determine why something does not work as expected and how to resolve the problem. Certain common techniques can help with the task of troubleshooting.

The first step in the troubleshooting process is to describe the problem completely. Problem descriptions help you and the {{site.data.keyword.IBM_notm}} technical-support representative know where to start to find the cause of the problem. This step includes asking yourself basic questions:

- What are the symptoms of the problem?
- Where does the problem occur?
- When does the problem occur?
- Under which conditions does the problem occur?
- Can the problem be reproduced?

The answers to these questions typically lead to a good description of the problem, which can then lead you to a problem resolution.

### What are the symptoms of the problem?

When you start to describe a problem, the most obvious question is **What is the problem?** This question might seem straightforward; however, you can break it down into several more-focused questions that create a more descriptive picture of the problem. These questions can include the following,

- Who, or what, is reporting the problem?
- What are the error codes and messages?
- How does the system fail? For example, is it a loop, hang, crash, performance degradation, or incorrect result?

### Where does the problem occur?

Determining where the problem originates is not always easy, but it is one of the most important steps in resolving a problem. Many layers of technology can exist between the reporting and failing components. Networks, disks, and drivers are only a few of the components to consider when you are investigating problems.

The following questions help you to focus on where the problem occurs to isolate the problem layer:

- Is the problem specific to one platform or operating system, or is it common across multiple platforms or operating systems?
- Is the current environment and configuration supported?
- Do all users have the problem?
- (For multi-site installations.) Do all sites have the problem?

If one layer reports the problem, the problem does not necessarily originate in that layer. Part of identifying where a problem originates is understanding the environment in which it exists. Take some time to completely describe the problem environment, including the operating system and version, all corresponding software and versions, and hardware information. Confirm that you are running within an environment that is a supported configuration, many problems can be traced back to incompatible levels of software that are not intended to run together or are not fully tested together.

### When does the problem occur?

Develop a detailed timeline of events that lead up to a failure, especially for those cases that are one-time occurrences. You can most easily develop a timeline by working backward: Start at the time an error was reported (as precisely as possible, even down to the millisecond), and work backward through the available logs and information. Typically, you need to look only as far as the first suspicious event that you find in a diagnostic log.

To develop a detailed timeline of events, answer these questions:

- Does the problem happen only at a certain time of day or night?
- How often does the problem happen?
- What sequence of events leads up to the time that the problem is reported?
- Does the problem happen after an environment change, such as upgrading or installing software or hardware?

Responding to these types of questions can give you a frame of reference in which to investigate the problem.

### Under which conditions does the problem occur?

Knowing which systems and applications are running at the time that a problem occurs is an important part of troubleshooting. These questions about your environment can help you to identify the root cause of the problem:

- Does the problem always occur when the same task is being performed?
- Does a certain sequence of events need to happen for the problem to occur?
- Do any other applications fail at the same time?

Answering these types of questions can help you explain the environment in which the problem occurs and correlate any dependencies. Just because multiple problems occurred around the same time, the problems are not necessarily related.

### Can the problem be reproduced?

From a troubleshooting standpoint, the ideal problem is one that can be reproduced. Typically, when a problem can be reproduced you have a larger set of tools or procedures at your disposal to help you investigate. Therefore, problems that you can reproduce are often easier to debug and solve.

However, problems that you can reproduce can have a disadvantage: If the problem is of significant business impact, you do not want it to recur. If possible, re-create the problem in a test or development environment, which typically offers you more flexibility and control during your investigation.

- Can the problem be re-created on a test system?
- Are multiple users or applications encountering the same type of problem?
- Can the problem be re-created by running a single command, a set of commands, or a particular application?

## Getting help and support for {{site.data.keyword.mobilefoundation_short}}
{: #getting_help_mobilefoundation}

If you have problems or questions when you use {{site.data.keyword.mobilefoundation_short}}, you can get help by searching for information or by asking questions through a forum. You can also open a support ticket.

When you use the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.

If you have technical questions about developing or deploying an app with {{site.data.keyword.mobilefoundation_short}}, post your question on [Stack Overflow](https://stackoverflow.com/search?q=%5B*worklight*%5D+or+%5B*mobilefirst*%5D+is%3Aquestion){: external}.

For more information about opening an IBM support ticket or about support levels and ticket severities, see [Contacting support](https://cloud.ibm.com/docs/get-support?topic=get-support-getting-customer-support).

Get product support by the way of [IBM's Support Portal](https://www-947.ibm.com/support/entry/myportal/support?brandind=other%20software). As a customer you can open support calls, review published security bulletins, be informed of released interim fixes, register for support notifications and more.

### MustGather documents

Review the MustGather documents before you open a support ticket.

The term **MustGather** represents the diagnostic data, which includes the system information, symptoms, log files, traces, etc. that is required to resolve a problem. By collecting MustGather data early, even before you open a PMR or a support ticket, you help IBM Support quickly determine the following information if:

* Symptoms match known problems (rediscovery).
* You have a non-defect problem that can be identified and resolved.
* There is a defect that identifies a work-around to reduce severity.
* Locating the root cause can speed development of a code fix.

#### Collecting the correct information

Problems in {{site.data.keyword.mobilefoundation_short}} can involve the following different parts:

* Application Center and {{site.data.keyword.mobilefoundation_short}} or {{site.data.keyword.mobilefoundation_short}} server on an Application Server or [IBM Cloud](#x7301758){: term}.
* Applications running on client devices.
It is important to collect the MustGather information from each part that is related to your problem. When in doubt, collect the MustGather information from all the parts.

If you are asked to collect more logs while re-creating a problem, you might be asked to collect logs you already collected. This is to ensure that support can see the entire scope of the re-created problem across a set of matching logs.

The following information is some tips for collecting MustGather information that apply to any problem:

* Describe the desired function, flows, and the error symptoms.
* Describe when and what changes were made between the time when everything was working correctly and when the problem occurred.
* Describe the simplest test case that reproduces the problem and provide the MustGather information for the test case.
* Provide accurate and specific times for when the problem shows itself in the MustGather materials.
* Describe how frequently the problem occurs and whether there are any triggering events for the problem.
* Describe any temporary circumventions or repairs for the problem, such as restarting the server.
* Describe the environment in which the problem occurs, including the versions of the components that are involved. Examples include client device, proxies, firewalls, {{site.data.keyword.mobilefoundation_short}} server application servers (including nodes and cells), databases, back-end servers, etc.


#### {{site.data.keyword.mobilefoundation_short}} CLI
{: #troubleshooting-mf-cli}
To collect the debug information to send to support, you can use the following steps for your platform to output the contents of the terminal to a file in the same directory.

* MacOS and Linux.
  ```bash
  mfp COMMAND -d 2>&1|tee cliOuput.log
  ```
  {: codeblock}
* Windows
  ```bash
  powershell
  mfp COMMAND -d 2>&1 | tee cliOutput.log
  exit
  ```
  {: codeblock}
Microsoft, Windows, Windows NT, and the Windows logo are trademarks of Microsoft Corporation in the United States, other countries, or both.
The -dd flag is preferred, if it is available for the version in use.
{: note}

| Version |	Debug Flag | Flag Description |	Full Command |
|---------|------------|------------------|--------------|
| 8.0.0	| -d, --debug	| Debug mode produces debug log output	| mfpdev -d |
| 8.0.0	| -dd, --ddebug |	Debug mode produces verbose log output |	mfpdev -dd |

#### Client applications

If the client is a web browser, provide the following information:

* Describe the client and browser version.
* Open the debugger of the browser and copy the contents of the console to a file that you include in the MustGather materials.

If the client is a mobile device, describe the device, including:

* Is it a physical device or emulator?
* What is the make of the device? For example, Apple, Samsung, HTC, or other device.
* What is the model and version of the device?
* What is the version of the operating system on the device?
  * On Apple iOS devices, click **Settings → General → About → Version**.
  * On Google Android devices, click **Settings → About phone → Software information → Android version**.
  * On Windows Phone devices, click **Settings → About → More info**.
* Is the device stock or has it been rooted?
* Have you tried multiple devices? Then, note the results for each device. For example, *It works on Apple iPhones that are running iOS 4 and Google Android that is phones running 3.0, but not on Android phones that are running 2.2.*

##### Google Android

On the Google Android platform, capture the debug messages for the device by running the Android Debug Bridge (ADB) logcat command on a workstation that is attached to the device with a USB cable. ADB is included in the installation of the Android Developer Tools.

You can run the following command that is appropriate for your workstation from a command-line that is running in the platform-tools directory where the android SDK is installed.

Administrator or root privileges might be required to successfully run logcat.

* For Microsoft Windows operating systems,
  ```bash
  adb.exe logcat -d -v time >logcat.txt
  ```
  {: codeblock}
* For Linux operating systems, 
  ```bash
  ./adb logcat -d -v time>logcat.txt
  ```
  {: codeblock}
Collect the logcat.txt file that is created as part of the MustGather materials.
You can find the documentation for [logcat](http://developer.android.com/tools/help/logcat.html){: external} on the Android Developers site.

##### Apple iOS

If you are using the Apple iOS platform, you can copy the log files by using Xcode Organizer. To access the Organizer, navigate to **Window → Organizer → Select Device → Device Logs**. Then, copy the device log files as part of the MustGather materials.

You can find additional information on collecting diagnostic information in the [Debugging Deployed iOS Apps](https://developer.apple.com/library/ios/qa/qa1747/_index.html){: external} topic within the iOS Developer Library.



