---

copyright:
  years: 2020
lastupdated: "2020-04-23"

keywords: JSONStore, offline storage, add jsonstore to android, jsonstore methods, jsonstore operations, access to documents, collection, offline storage configuration

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
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Configure offline storage
{: #configure_offline_storage_android}

The {{site.data.keyword.mobilefoundation_short}} JSONStore is an optional client-side API that provides a lightweight, document-oriented storage system. JSONStore enables persistent storage of [JSON](#x4267096){: term} documents. Documents in an application are available in JSONStore even when the device that is running the application is offline. This persistent, always-available storage can be useful to give users access to documents when, for example, there's no network connection available in the device. For an overview of JSONStore concepts and terminology, see [here](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-jsonstore#jsonstore).

## Configure offline storage for Android apps
{: #adding_offline_storage_android}


Make sure that the {{site.data.keyword.mobilefoundation_short}} Native SDK was added to the Android Studio project.

Follow the [Adding the {{site.data.keyword.mobilefoundation_short}} SDK to Android applications](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/application-development/sdk/android/){: external} tutorial.
{: tip}

### Adding JSONStore to your Android project
{: #adding_jsonstore_android}
{: help}
{: support}

1. From **Android → Gradle Scripts**, select the `build.gradle (Module: app)` file.
2. Add the following to the existing `dependencies` section:

   ```bash
   compile 'com.ibm.mobile.foundation:ibmmobilefirstplatformfoundationjsonstore:8.0.+'
   ```
   {: codeblock}

3. Add the following to the `DefaultConfig` section of your `build.gradle` file:

   ```gradle
   ndk {
     abiFilters "armeabi", "armeabi-v7a", "x86", "mips"
   }
   ```
   {: codeblock}
   
   Add the `abiFilters` to ensure that the apps with JSONStore run in any of the previously specified architectures. This is required as JSONStore depends on a third-party library that supports only these architectures.
   {: note}
   
### Open an Android JSONStore collection
{: #open_android}

Use `openCollections` to open one or more JSONStore collections.

```java
Context context = getContext();
try {
  JSONStoreCollection people = new JSONStoreCollection("people");
  people.setSearchField("name", SearchFieldType.STRING);
  people.setSearchField("age", SearchFieldType.INTEGER);
  List<JSONStoreCollection> collections = new LinkedList<JSONStoreCollection>();
  collections.add(people);
  WLJSONStore.getInstance(context).openCollections(collections);
  // handle success
} catch(JSONStoreException e) {
  // handle failure
}
```
{: codeblock}

### Get an accessor to your Android JSONStore collection
{: #get_jsonstore_android}

Use `getCollectionByName` to create an accessor to the collection. You must call `openCollections` before you call `getCollectionByName`.

```java
Context context = getContext();
try {
  String collectionName = "people";
  JSONStoreCollection collection = WLJSONStore.getInstance(context).getCollectionByName(collectionName);
  // handle success
} catch(JSONStoreException e) {
  // handle failure
}
```
{: codeblock}

The variable collection can now be used to perform operations on the `people` collection such as `add`, `find`, and `replace`.

### Add documents to an Android collection
{: #add_jsonstore_android}

Use `addData` to store data as documents inside a collection.

```java
Context context = getContext();
try {
  String collectionName = "people";
  JSONStoreCollection collection = WLJSONStore.getInstance(context).getCollectionByName(collectionName);
  //Add options.
  JSONStoreAddOptions options = new JSONStoreAddOptions();
  options.setMarkDirty(true);
  JSONObject data = new JSONObject("{age: 23, name: 'yoel'}")
  collection.addData(data, options);
  // handle success
} catch(JSONStoreException e) {
  // handle failure
}
```
{: codeblock}

### Find documents inside an Android collection
{: #find_jsonstore_android}

Use `findDocuments` to locate a document inside a collection by using a query. Use `findAllDocuments` to retrieve all the documents inside a collection. Use `findDocumentById` to search by the document unique identifier..

```java
Context context = getContext();
try {
  String collectionName = "people";
  JSONStoreQueryPart queryPart = new JSONStoreQueryPart();
  // fuzzy search LIKE
  queryPart.addLike("name", name);
  JSONStoreQueryParts query = new JSONStoreQueryParts();
  query.addQueryPart(queryPart);
  JSONStoreFindOptions options = new JSONStoreFindOptions();
  // returns a maximum of 10 documents, default: returns every document
  options.setLimit(10);
  JSONStoreCollection collection = WLJSONStore.getInstance(context).getCollectionByName(collectionName);
  List<JSONObject> results = collection.findDocuments(query, options);
  // handle success
} catch(JSONStoreException e) {
  // handle failure
}
```
{: codeblock}

### Replace documents inside an Android collection
{: #replace_jsonstore_android}

Use `replaceDocuments` to modify documents inside a collection. The field that you use to perform the replacement is `_id`, the document unique identifier.

```java
Context context = getContext();
try {
  String collectionName = "people";
  JSONStoreCollection collection = WLJSONStore.getInstance(context).getCollectionByName(collectionName);
  JSONStoreReplaceOptions options = new JSONStoreReplaceOptions();
  // mark data as dirty
  options.setMarkDirty(true);
  JSONStore replacement = new JSONObject("{_id: 1, json: {age: 23, name: 'chevy'}}");
  collection.replaceDocument(replacement, options);
  // handle success
} catch(JSONStoreException e) {
  // handle failure
}
```
{: codeblock}

This example assumes that the document `{_id: 1, json: {name: 'yoel', age: 23} }` is in the collection.

### Remove documents from an Android collection
{: #remove_jsonstore_android}

Use `removeDocumentById` to delete a document from a collection. Documents aren’t erased from the collection until you call `markDocumentClean`.

```java
Context context = getContext();
try {
  String collectionName = "people";
  JSONStoreCollection collection = WLJSONStore.getInstance(context).getCollectionByName(collectionName);
  JSONStoreRemoveOptions options = new JSONStoreRemoveOptions();
  // Mark data as dirty
  options.setMarkDirty(true);
  collection.removeDocumentById(1, options);
  // handle success
} catch(JSONStoreException e) {
  // handle failure
}
```
{: codeblock}

### Remove an entire Android collection
{: #remove_collection_jsonstore_android}

Use `removeCollection` to delete all the documents that are stored inside a collection. This operation is similar to dropping a table in database terms.

```java
Context context = getContext();
try {
  String collectionName = "people";
  JSONStoreCollection collection = WLJSONStore.getInstance(context).getCollectionByName(collectionName);
  collection.removeCollection();
  // handle success
} catch(JSONStoreException e) {
  // handle failure
}
```
{: codeblock}

### Destroy an Android JSONStore
{: #destroy_jsonstore_android}

Use `destroy` to remove the following data:
* All documents
* All collections
* All Stores
* All JSONStore metadata and security artifacts

```java
Context context = getContext();
try {
  WLJSONStore.getInstance(context).destroy();
  // handle success
} catch(JSONStoreException e) {
  // handle failure
}
```
{: codeblock}

## Next steps
{: #next-steps-android-js}

* [Learn more about JSONStore](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-jsonstore).
* [Advanced offline storage configuration](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-advanced_jsonstore#advanced_jsonstore).
* [Add {{site.data.keyword.mobilefoundation_short}} Analytics](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-instrument_your_app_android).
* [Send in-app feedback](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-sending_in_app_user_feedback_android).
* [Receive Push Notifications](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-receiving_push_notifications_in_android).

