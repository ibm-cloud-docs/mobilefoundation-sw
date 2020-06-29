---

copyright:
  years: 2020
lastupdated: "2020-04-30"

keywords: JSONStore, offline storage, add jsonstore to reactnative, jsonstore methods, jsonstore operations, access to documents, collection, offline storage configuration

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
{: #configure_offline_storage_reactnative}

The {{site.data.keyword.mobilefoundation_short}} JSONStore is an optional client-side API that provides a lightweight, document-oriented storage system. JSONStore enables persistent storage of [JSON](#x4267096){: term} documents. Documents in an application are available in JSONStore even when the device that is running the application is offline. This persistent, always-available storage can be useful to give users access to documents when, for example, there's no network connection available in the device. For an overview of JSONStore concepts and terminology, see [here](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-jsonstore#jsonstore).

## Adding offline storage for React Native apps
{: #adding_offline_storage_reactnative}
{: help}
{: support}

1. Open a command-line terminal and navigate to your React Native project folder.

2. Run the following command.

   ```bash
   npm install react-native-ibm-mobilefirst-jsonstore --save
   ```
   {: codeblock}

3. [**iOS only**] Install {{site.data.keyword.mobilefoundation_short}} pod dependencies.

   ```bash
   cd ios && pod install
   ```
   {: codeblock}

## Basic Usage
{: #basic_usage_reactnative}

### Creating a new JSONStore Collection

1. Use `JSONStoreCollection` class to create instances of JSONStore. You can also set more configuration to this newly created JSONStore Collection (for example, setting search fields).

2. To start interacting with an existing JSONStore collection (for example: adding or removing data) you need to *Open* the collection. Use `openCollections()` API to open the collection.
   ```javascript
   var collection = new JSONStoreCollection('people');
    WLJSONStore.openCollections(['people'])
    .then(res => {
      // handle success
    }).catch(err => {
      // handle failure
    });
   ``` 
   {: codeblock}

### Add data in a JSONStore collection

Use `addData()` API to store JSON Data in a collection.

```javascript
var data = { "name": "John", age: 28 };
var collection = new JSONStoreCollection('people');
collection.addData(data)
.then(res => {
  // handle success
}).catch(err => {
  // handle failure
});
```
{: codeblock}

You can add a single JSON object or an Array of JSON objects by using this API.
{: tip}

### Find data in a JSONStore collection

1. Use `find` to locate a document inside a collection by using a query.
2. Use `findAllDocuments()` API for retrieving all the documents inside a collection.
3. Use `findDocumentById()` and `findDocumentsById()` API to search by using the document unique identifier.
4. Use `findDocuments()` API to query the collection. For querying, you can use `JSONStoreQueryPart` class objects to filter the data.

Pass an array of `JSONStoreQueryPart` objects as a parameter to findDocuments API.

```javascript
var collection = new JSONStoreCollection('people');
var query = new JSONStoreQueryPart();
query.addEqual("name", "John");
collection.findDocuments([query])
.then(res => {
	// handle success
}).catch(err => {
	// handle failure
});
```
{: codeblock}

### Remove data from a JSONStore collection

Use `remove` to delete a document from a collection.

```javascript
var id = 1; // for example
var collection = new JSONStoreCollection('people');
collection.removeDocumentById(id)
.then(res => {
	// handle success
}).catch(err => {
	// handle failure     
});
```

### Remove a JSONStore collection

Use `removeCollection` to delete all the documents that are stored inside a collection. This operation is similar to dropping a table in database terms.

```javascript
var collection = new JSONStoreCollection('people');
collection.removeCollection()
.then(res => {
	// handle success
}).catch(err => {
	// handle failure
});
```

## Next steps
{: #next-steps-reactnative-js}

* [Learn more about JSONStore](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-jsonstore).
* [Advanced offline storage configuration](/docs/mobilefoundation-sw?topic=mobilefoundation-sw-advanced_jsonstore#advanced_jsonstore).

