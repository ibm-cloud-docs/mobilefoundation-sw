---

copyright:
  years: 2020
lastupdated: "2020-04-23"

keywords: JSONStore, offline storage, add jsonstore to cordova, jsonstore methods, jsonstore operations, access to documents, collection, offline storage configuration

subcollection:  mobilefoundation-sw

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:term: .term}
{:important: .important}
{:note: .note}
{:download: .download}
{:external: target="_blank" .external}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Configure offline storage
{: #configure_offline_storage_cordova}

The {{site.data.keyword.mobilefoundation_short}} JSONStore is an optional client-side API that provides a lightweight, document-oriented storage system. JSONStore enables persistent storage of [JSON](#x4267096){: term} documents. Documents in an application are available in JSONStore even when the device that is running the application is offline. This persistent, always-available storage can be useful to give users access to documents when, for example, there's no network connection available in the device. For an overview of JSONStore concepts and terminology, see [here](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-jsonstore#jsonstore).

## Configure offline storage for Cordova or Ionic apps
{: #configure_offline_storage_cordova_ionic}

Make sure the {{site.data.keyword.mobilefoundation_short}} Cordova SDK was added to the project.

Follow the [Adding the {{site.data.keyword.mobilefoundation_short}} SDK to Cordova applications](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/application-development/sdk/cordova/){: external} tutorial.
{: tip}

### Adding JSONStore to your Cordova project
{: #adding_jsonstore_cordova}
{: help
{: support}


1. Open a command line window and navigate to your Cordova project folder.
1. Run the command:

   ```bash
   cordova plugin add cordova-plugin-mfp-jsonstore
   ```
   {: codeblock}

### Initialize JSONStore collection
{: #initialize_jsonstore_cordova}   

Use `init` to start one or more JSONStore collections.
Starting or provisioning a collection means creating the persistent storage that contains the collection and documents, if it does not exist. If a password is passed to options, the persistent storage is encrypted with the password.

```javascript
var collections = {
    people : {
        searchFields: {name: 'string', age: 'integer'}
    }
};
WL.JSONStore.init(collections).then(function (collections) {
    // handle success - collection.people (people's collection)
}).fail(function (error) {
    // handle failure
});
```
{: codeblock}

### Get an accessor to your Cordova JSONStore collection
{: #get_jsonstore_cordova}

Use `get` to create an accessor to the collection. You must call `init` before you call `get` otherwise the result of `get` is *undefined*.

```javascript
var collectionName = 'people';
var people = WL.JSONStore.get(collectionName);
```
{: codeblock}

The variable *people* can now be used to perform operations on the *people* collection such as `add`, `find`, and `replace`.

### Add documents to a Cordova collection
{: #add_jsonstore_cordova}

Use `add` to store data as documents inside a collection.

```javascript
var collectionName = 'people';
var options = {};
var data = {name: 'yoel', age: 23};

WL.JSONStore.get(collectionName).add(data, options).then(function () {
    // handle success
}).fail(function (error) {
    // handle failure
});
```
{: codeblock}

### Find documents inside a Cordova collection
{: #find_jsonstore_cordova}

* Use `find` to locate a document inside a collection by using a query.
* Use `findAll` to retrieve all the documents inside a collection.
* Use `findById` to search by the document unique identifier.

The default behavior for find is to do a "fuzzy" search.

```javascript
var query = {name: 'yoel'};
var collectionName = 'people';
var options = {
  exact: false, //default
  limit: 10 // returns a maximum of 10 documents, default: return every document
};

WL.JSONStore.get(collectionName).find(query, options).then(function (results) {
    // handle success - results (array of documents found)
}).fail(function (error) {
    // handle failure
});
```
{: codeblock}

```javascript
var age = document.getElementById("findByAge").value || '';

if(age == "" || isNaN(age)){
  alert("Please enter a valid age to find");
}
else {
  query = {age: parseInt(age, 10)};
  var options = {
    exact: true,
    limit: 10 //returns a maximum of 10 documents
  };
  WL.JSONStore.get(collectionName).find(query, options).then(function (res) {
    // handle success - results (array of documents found)
  }).fail(function (errorObject) {
    // handle failure
  });
}
```
{: codeblock}

### Replace documents inside a Cordova collection
{: #replace_jsonstore_cordova}

Use `replace` to modify documents inside a collection. The field that you use to perform the replacement is `_id`, the document unique identifier.

```javascript
var document = {
  _id: 1, json: {name: 'chevy', age: 23}
};
var collectionName = 'people';
var options = {};

WL.JSONStore.get(collectionName).replace(document, options).then(function (numberOfDocsReplaced) {
    // handle success
}).fail(function (error) {
    // handle failure
});
```
{: codeblock}

This example assumes that the document `{_id: 1, json: {name: 'yoel', age: 23} }` is in the collection.

### Remove documents from a Cordova collection
{: #remove_jsonstore_cordova}

Use `remove` to delete a document from a collection.
Documents are not erased from the collection until you call push.

```javascript
var query = {_id: 1};
var collectionName = 'people';
var options = {exact: true};
WL.JSONStore.get(collectionName).remove(query, options).then(function (numberOfDocsRemoved) {
    // handle success
}).fail(function (error) {
    // handle failure
});
```
{: codeblock}

### Remove an entire Cordova collection
{: #remove_collection_jsonstore_cordova}

Use `removeCollection` to delete all the documents that are stored inside a collection. This operation is similar to dropping a table in database terms.

### Destroy Cordova JSONStore
{: #destroy_jsonstore_cordova}

Use `destroy` to remove the following data:
* All documents
* All collections
* All Stores
* All JSONStore metadata and security artifacts


## Next steps
{: #next-steps-cordova-js}

* [Learn more about JSONStore](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-jsonstore).
* [Advanced offline storage configuration](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-advanced_jsonstore#advanced_jsonstore).
* [Add {{site.data.keyword.mobilefoundation_short}} Analytics](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-instrument_your_app_cordova).
* [Send in-app feedback](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-sending_in_app_user_feedback_cordova).
* [Receive Push Notifications](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-receiving_push_notifications_in_cordova).
