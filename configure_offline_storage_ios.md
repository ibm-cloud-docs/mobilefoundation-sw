---

copyright:
  years: 2020
lastupdated: "2020-04-23"

keywords: JSONStore, offline storage, add jsonstore to ios, jsonstore methods, jsonstore operations, access to documents, collection, offline storage configuration

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
{: #configure_offline_storage_ios}

The {{site.data.keyword.mobilefoundation_short}} JSONStore is an optional client-side API that provides a lightweight, document-oriented storage system. JSONStore enables persistent storage of [JSON](#x4267096){: term} documents. Documents in an application are available in JSONStore even when the device that is running the application is offline. This persistent, always-available storage can be useful to give users access to documents when, for example, there's no network connection available in the device. For an overview of JSONStore concepts and terminology, see [here](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-jsonstore#jsonstore).

## Configure offline storage for iOS apps
{: #adding_offline_storage_ios}

Make sure that the {{site.data.keyword.mobilefoundation_short}} Native SDK was added to the Xcode project.


Follow the [Adding the {{site.data.keyword.mobilefoundation_short}} SDK to iOS applications](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/application-development/sdk/ios/){: external} tutorial.
{: tip}


### Adding JSONStore to your iOS project
{: #adding_jsonstore_ios}
{: help
{: support}

1. Add the following to the existing `podfile`, at the root of the Xcode project.

   ```bash
   pod 'IBMMobileFirstPlatformFoundationJSONStore'
   ```
   {: codeblock}
   

1. From command line, go to the root of the Xcode project and run the command:

   ```bash
   pod install
   ```
   {: codeblock}
   

1. Whenever you want to use JSONStore, make sure that you import the JSONStore header:

   **Objective-C**:
   ```objectivec
   #import <IBMMobileFirstPlatformFoundationJSONStore/IBMMobileFirstPlatformFoundationJSONStore.h>
   ```
   {: codeblock}

   **Swift:**
   ```swift
   import IBMMobileFirstPlatformFoundationJSONStore
   ```   
   {: codeblock}
   

### Open iOS JSONStore collection
{: #open_ios}


Use `openCollections` to open one or more JSONStore collections.


```swift
let collection:JSONStoreCollection = JSONStoreCollection(name: "people")

collection.setSearchField("name", withType: JSONStore_String)
collection.setSearchField("age", withType: JSONStore_Integer)

do {
  try JSONStore.sharedInstance().openCollections([collection], withOptions: nil)
} catch let error as NSError {
  // handle error
}
```
{: codeblock}


### Get an accessor to your iOS JSONStore collection
{: #get_jsonstore_ios}


Use `getCollectionWithName` to create an accessor to the collection. You must call `openCollections` before you call `getCollectionWithName`.


```swift
let collectionName:String = "people"
let collection:JSONStoreCollection = JSONStore.sharedInstance().getCollectionWithName(collectionName)
```
{: codeblock}


The variable collection can now be used to perform operations on the `people` collection such as `add`, `find`, and `replace`.


### Add documents to an iOS collection
{: #add_jsonstore_ios}


Use `addData` to store data as documents inside a collection.


```swift
let collectionName:String = "people"
let collection:JSONStoreCollection = JSONStore.sharedInstance().getCollectionWithName(collectionName)

let data = ["name" : "yoel", "age" : 23]

do  {
  try collection.addData([data], andMarkDirty: true, withOptions: nil)
} catch let error as NSError {
  // handle error
}
```
{: codeblock}


### Find documents inside an iOS collection
{: #find_jsonstore_ios}


Use `findWithQueryParts` to locate a document inside a collection by using a query. Use `findAllWithOptions` to retrieve all the documents inside a collection. Use `findWithIds` to search by the document unique identifier.


```swift
let collectionName:String = "people"
let collection:JSONStoreCollection = JSONStore.sharedInstance().getCollectionWithName(collectionName)

let options:JSONStoreQueryOptions = JSONStoreQueryOptions()
// returns a maximum of 10 documents, default: returns every document
options.limit = 10

let query:JSONStoreQueryPart = JSONStoreQueryPart()
query.searchField("name", like: "yoel")

do  {
  let results:NSArray = try collection.findWithQueryParts([query], andOptions: options)
} catch let error as NSError {
  // handle error
}
```
{: codeblock}


### Replace documents inside an iOS collection
{: #replace_jsonstore_ios}


Use `replaceDocuments` to modify documents inside a collection. The field that you use to perform the replacement is `_id`, the document unique identifier.


```swift
let collectionName:String = "people"
let collection:JSONStoreCollection = JSONStore.sharedInstance().getCollectionWithName(collectionName)

var document:Dictionary<String,AnyObject> = Dictionary()
document["name"] = "chevy"
document["age"] = 23

var replacement:Dictionary<String, AnyObject> = Dictionary()
replacement["_id"] = 1
replacement["json"] = document

do {
  try collection.replaceDocuments([replacement], andMarkDirty: true)
} catch let error as NSError {
  // handle error
}
```
{: codeblock}


This example assumes that the document `{_id: 1, json: {name: 'yoel', age: 23} }` is in the collection.


### Remove documents from an iOS collection
{: #remove_jsonstore_ios}


Use `removeWithIds` to delete a document from a collection. Documents aren’t erased from the collection until you call `markDocumentClean`.


```swift
let collectionName:String = "people"
let collection:JSONStoreCollection = JSONStore.sharedInstance().getCollectionWithName(collectionName)

do {
  try collection.removeWithIds([1], andMarkDirty: true)
} catch let error as NSError {
  // handle error
}
```
{: codeblock}


### Remove an entire iOS collection
{: #remove_collection_jsonstore_ios}


Use `removeCollection` to delete all the documents that are stored inside a collection. This operation is similar to dropping a table in database terms.


```swift
let collectionName:String = "people"
let collection:JSONStoreCollection = JSONStore.sharedInstance().getCollectionWithName(collectionName)

do {
  try collection.removeCollection()
} catch let error as NSError {
  // handle error
}
```
{: codeblock}


### Destroy an iOS JSONStore
{: #destroy_jsonstore_ios}


Use `destroyData` to remove the following data:
* All documents
* All collections
* All Stores
* All JSONStore metadata and security artifacts


```swift
do {
  try JSONStore.sharedInstance().destroyData()
} catch let error as NSError {
  // handle error
}
```
{: codeblock}

## Next steps
{: #next-steps-ios-js}

* [Learn more about JSONStore](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-jsonstore).
* [Advanced offline storage configuration](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-advanced_jsonstore#advanced_jsonstore).
* [Add {{site.data.keyword.mobilefoundation_short}} Analytics](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-instrument_ios_app).
* [Send in-app feedback](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-sending_in_app_user_feedback_ios).
* [Receive Push Notifications](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-receiving_push_notifications_in_ios).


