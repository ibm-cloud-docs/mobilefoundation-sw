---

copyright:
  years: 2020
lastupdated: "2020-04-29"

keywords: JSONStore, advanced jsonstore, Cordova secure jsonstore, iOS secure jsonstore, android jsonstore, Data encryption, multiple stores, adapter integration, mobile app development

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

# Advanced JSONStore
{: #advanced_jsonstore}

## Security in JSONStore
{: #security_jsonstore}

You can secure all the collections in a store by passing a password to the `init` function. If no password is passed, the documents of all the collections in the store are not encrypted.
{: cordova}

Data encryption is only available on Android, iOS, Windows 8.1 Universal and Windows 10 UWP environments. 

><cite>Microsoft, Windows, Windows NT, and the Windows logo are trademarks of Microsoft Corporation in the United States, other countries, or both.</cite>

Some security metadata is stored in the keychain (iOS), shared preferences (Android), or the credential locker (Windows 8.1).
The store is encrypted with a 256-bit Advanced Encryption Standard (AES) key. All keys are strengthened with Password-Based Key Derivation Function 2 (PBKDF2).
{: cordova}

Use `closeAll` to lock access to all the collections until you call `init` again. If you think of `init` as a login function, you can think of `closeAll` as the corresponding logout function. Use `changePassword` to change the password.
{: cordova}

Encryption is supported in iOS only. By default, the {{site.data.keyword.mobilefoundation_short}} Cordova SDK for iOS relies on iOS provided APIs for encryption. If you prefer to replace this with OpenSSL:
{: cordova}

* Add the `cordova-plugin-mfp-encrypt-utils` plug-in:

   ```bash
   cordova plugin add cordova-plugin-mfp-encrypt-utils.
   ```
   {: codeblock}

* In the application logic, use: `WL.SecurityUtils.enableNativeEncryption(false)` to enable the OpenSSL option.
{: cordova}

You can secure all the collections in a store by passing a `JSONStoreOpenOptions` object with a password to the `openCollections` function. If no password is passed, the documents of all the collections in the store aren’t encrypted.
{: ios}

Some security metadata is stored in the keychain (iOS).
The store is encrypted with a 256-bit Advanced Encryption Standard (AES) key. All keys are strengthened with Password-Based Key Derivation Function 2 (PBKDF2).
{: ios}

Use `closeAllCollections` to lock access to all the collections until you call `openCollections` again. If you think of `openCollections` as a login function, you can think of `closeAllCollections` as the corresponding logout function.
{: ios}

Use `changeCurrentPassword` to change the password.
{: ios}

```swift
let collection:JSONStoreCollection = JSONStoreCollection(name: "people")
collection.setSearchField("name", withType: JSONStore_String)
collection.setSearchField("age", withType: JSONStore_Integer)

let options:JSONStoreOpenOptions = JSONStoreOpenOptions()
options.password = "123"

do {
  try JSONStore.sharedInstance().openCollections([collection], withOptions: options)
} catch let error as NSError {
  // handle error
}
```
{: codeblock}
{: ios}

You can secure all the collections in a store by passing a `JSONStoreInitOptions` object with a password to the `openCollections` function. If no password is passed, the documents of all the collections in the store are not encrypted.
{: android}

Some security metadata is stored in the shared preferences (Android).
The store is encrypted with a 256-bit Advanced Encryption Standard (AES) key. All keys are strengthened with Password-Based Key Derivation Function 2 (PBKDF2).
{: android}

Use `closeAllCollections` to lock access to all the collections until you call `openCollections` again. If you think of `openCollections` as a login function, you can think of `closeAllCollections` as the corresponding logout function.
{: android}

Use `changeCurrentPassword` to change the password.
{: android}

```java
Context context = getContext();
try {
  JSONStoreCollection people = new JSONStoreCollection("people");
  people.setSearchField("name", SearchFieldType.STRING);
  people.setSearchField("age", SearchFieldType.INTEGER);
  List<JSONStoreCollection> collections = new LinkedList<JSONStoreCollection>();
  collections.add(people);
  JSONStoreInitOptions options = new JSONStoreInitOptions();
  options.setPassword("123");
  WLJSONStore.getInstance(context).openCollections(collections, options);
  // handle success
} catch(JSONStoreException e) {
  // handle failure
}
```
{: codeblock}
{: android}

## Support for Multiple users in JSONStore
{: #multiple_user_jsonstore}

You can create multiple stores that contain different collections in a single {{site.data.keyword.mobilefoundation_short}} application. The `init` function can take an options object with a username. If no username is given, the default username is *jsonstore*.
{: cordova}

```javascript
var collections = {
  people: {
    searchFields: {name: 'string'}
  }
};
var options = {username: 'yoel'};
WL.JSONStore.init(collections, options).then(function () {
    // handle success
}).fail(function (error) {
    // handle failure
});
```
{: codeblock}
{: cordova}

You can create multiple stores that contain different collections in a single {{site.data.keyword.mobilefoundation_short}} application. The `init` function can take an options object with a username. If no username is given, the default username is *jsonstore*.
{: ios}

```swift
let collection:JSONStoreCollection = JSONStoreCollection(name: "people")
collection.setSearchField("name", withType: JSONStore_String)
collection.setSearchField("age", withType: JSONStore_Integer)

let options:JSONStoreOpenOptions = JSONStoreOpenOptions()
options.username = "yoel"

do {
  try JSONStore.sharedInstance().openCollections([collection], withOptions: options)
} catch let error as NSError {
  // handle error
}
```
{: codeblock}
{: ios}

You can create multiple stores that contain different collections in a single {{site.data.keyword.mobilefoundation_short}} application. The `openCollections` function can take an options object with a username. If no username is given, the default username is *jsonstore*.
{: android}

```java
Context context = getContext();
try {
  JSONStoreCollection people = new JSONStoreCollection("people");
  people.setSearchField("name", SearchFieldType.STRING);
  people.setSearchField("age", SearchFieldType.INTEGER);
  List<JSONStoreCollection> collections = new LinkedList<JSONStoreCollection>();
  collections.add(people);
  JSONStoreInitOptions options = new JSONStoreInitOptions();
  options.setUsername("yoel");
  WLJSONStore.getInstance(context).openCollections(collections, options);
  // handle success
} catch(JSONStoreException e) {
  // handle failure
}
```
{: codeblock}
{: android}

## Adapter integration
{: #adapter_integration}

Adapter integration is optional and provides ways to send data from a collection to an adapter and get data from an adapter into a collection.
You can achieve these goals by using `WLResourceRequest` or `jQuery.ajax` if you need more flexibility.
{: cordova}

1. Create an adapter and name it **JSONStoreAdapter**.
1. Define its procedures `addPerson`, `getPeople`, `pushPeople`, `removePerson`, and `replacePerson`.

   ```javascript
   function getPeople() {
    var data = { peopleList : [{name: 'chevy', age: 23}, {name: 'yoel', age: 23}] };
    WL.Logger.debug('Adapter: people, procedure: getPeople called.');
    WL.Logger.debug('Sending data: ' + JSON.stringify(data));
    return data;
    }
    function pushPeople(data) {
        WL.Logger.debug('Adapter: people, procedure: pushPeople called.');
        WL.Logger.debug('Got data from JSONStore to ADD: ' + data);
        return;
    }
    function addPerson(data) {
        WL.Logger.debug('Adapter: people, procedure: addPerson called.');
        WL.Logger.debug('Got data from JSONStore to ADD: ' + data);
        return;
    }
    function removePerson(data) {
        WL.Logger.debug('Adapter: people, procedure: removePerson called.');
        WL.Logger.debug('Got data from JSONStore to REMOVE: ' + data);
        return;
    }
    function replacePerson(data) {
        WL.Logger.debug('Adapter: people, procedure: replacePerson called.');
        WL.Logger.debug('Got data from JSONStore to REPLACE: ' + data);
        return;
    }
   ```
   {: cordova}

1. To load data from an adapter use `WLResourceRequest`.
   ```javascript
   try {
     var resource = new WLResourceRequest("adapters/JSONStoreAdapter/getPeople", WLResourceRequest.GET);
     resource.send()
     .then(function (responseFromAdapter) {
          var data = responseFromAdapter.responseJSON.peopleList;
     },function(err){
          //handle failure
     });
    } catch (e) {
        alert("Failed to load data from adapter " + e.Messages);
    }
   ```
   {: cordova}   

1. Calling `getPushRequired` returns an array of so called "dirty documents", which are documents that have local modifications that do not exist on the back-end system. These documents are sent to the adapter when `push` is called.

   ```javascript
   var collectionName = 'people';
   WL.JSONStore.get(collectionName).getPushRequired().then(function (dirtyDocuments) {
        // handle success
   }).fail(function (error) {
      // handle failure
   });
   ```
   {: codeblock}
   {: cordova}

   To prevent JSONStore from marking the documents as "dirty", pass the option `{markDirty:false}` to `add`, `replace`, and `remove`.
   {: tip}
   {: cordova}

1. You can also use the `getAllDirty` API to retrieve the dirty documents.

   ```javascript
   WL.JSONStore.get(collectionName).getAllDirty()
    .then(function (dirtyDocuments) {
        // handle success
    }).fail(function (errorObject) {
        // handle failure
    });
   ```
   {: codeblock}
   {: cordova}

1. To push changes to an adapter, call the `getAllDirty` to get a list of documents with modifications and then use `WLResourceRequest`. After the data is sent and a successful response is received make sure, you call `markClean`.

   ```javascript
   try {
     var collectionName = "people";
     var dirtyDocs;

     WL.JSONStore.get(collectionName)
     .getAllDirty()
     .then(function (arrayOfDirtyDocuments) {
        dirtyDocs = arrayOfDirtyDocuments;

        var resource = new WLResourceRequest("adapters/JSONStoreAdapter/pushPeople", WLResourceRequest.POST);
        resource.setQueryParameter('params', [dirtyDocs]);
        return resource.send();
        }).then(function (responseFromAdapter) {
            return WL.JSONStore.get(collectionName).markClean(dirtyDocs);
        }).then(function (res) {
          //handle success     
        }).fail(function (errorObject) {
          // Handle failure.
        });

    } catch (e) {
        alert("Failed To Push Documents to Adapter");
    }
   ```
   {: codeblock}
   {: cordova}

1. Use `enhance` to extend the core API to fit your needs, by adding functions to a collection prototype. This example (the following code snippet) shows how to use `enhance` to add the function `getValue` that works on the `keyvalue` collection. It takes a key (string) as it's only parameter and returns a single result.

   ```javascript
   var collectionName = 'keyvalue';
    WL.JSONStore.get(collectionName).enhance('getValue', function (key) {
        var deferred = $.Deferred();
        var collection = this;
        //Do an exact search for the key
        collection.find({key: key}, {exact:true, limit: 1}).then(deferred.resolve, deferred.reject);
        return deferred.promise();
    });

    //Usage:
    var key = 'myKey';
    WL.JSONStore.get(collectionName).getValue(key).then(function (result) {
        // handle success
        // result contains an array of documents with the results from the find
    }).fail(function () {
        // handle failure
    });
   ```
   {: codeblock}
   {: cordova}

1. See the JSONStore sample for Cordova app from the **Samples** section. This project contains a Cordova application that uses the JSONStore API set. JavaScript adapter Maven project can be downloaded from [here](https://github.com/MobileFirst-Platform-Developer-Center/JSONStoreAdapter/tree/release80).
{: cordova}

Adapter integration is optional and provides ways to send data from a collection to an adapter and get data from an adapter into a collection.
You can achieve these goals by using `WLResourceRequest`.
{: ios}

1. Create an adapter and name it **People**.
1. Define it's procedures `addPerson`, `getPeople`, `pushPeople`, `removePerson`, and `replacePerson`.
1. To load data from an adapter use `WLResourceRequest`.

   ```swift
    // Start - LoadFromAdapter
    class LoadFromAdapter: NSObject, WLDelegate {
      func onSuccess(response: WLResponse!) {
        let responsePayload:NSDictionary = response.getResponseJson()
        let people:NSArray = responsePayload.objectForKey("peopleList") as! NSArray
        // handle success
      }

      func onFailure(response: WLFailResponse!) {
        // handle failure
      }
    }
    // End - LoadFromAdapter

    let pull = WLResourceRequest(URL: NSURL(string: "/adapters/People/getPeople"), method: "GET")

    let loadDelegate:LoadFromAdapter = LoadFromAdapter()
    pull.sendWithDelegate(loadDelegate)
   ```
   {: codeblock}
   {: ios}

1. Calling `allDirty` returns an array of so called "dirty documents", which are documents that have local modifications that don’t exist on the back-end system.

   ```swift
    let collectionName:String = "people"
    let collection:JSONStoreCollection = JSONStore.sharedInstance().getCollectionWithName(collectionName)

    do {
      let dirtyDocs:NSArray = try collection.allDirty()
    } catch let error as NSError {
      // handle error
    }
   ```
   {: codeblock}
   {: ios}

   To prevent JSONStore from marking the documents as "dirty", pass the option `{markDirty:false}` to `add`, `replace`, and `remove`.
   {: tip}

1. To push changes to an adapter, call the `allDirty` to get a list of documents with modifications and then use `WLResourceRequest`. After the data is sent and a successful response is received make sure, you call `markDocumentsClean`.

   ```swift
    // Start - PushToAdapter
    class PushToAdapter: NSObject, WLDelegate {
      func onSuccess(response: WLResponse!) {
        // handle success
      }

      func onFailure(response: WLFailResponse!) {
        // handle failure
      }
    }
    // End - PushToAdapter

    let collectionName:String = "people"
    let collection:JSONStoreCollection = JSONStore.sharedInstance().getCollectionWithName(collectionName)

    do {
      let dirtyDocs:NSArray = try collection.allDirty()
      let pushData:NSData = NSKeyedArchiver.archivedDataWithRootObject(dirtyDocs)

      let push = WLResourceRequest(URL: NSURL(string: "/adapters/People/pushPeople"), method: "POST")

      let pushDelegate:PushToAdapter = PushToAdapter()
      push.sendWithData(pushData, delegate: pushDelegate)

    } catch let error as NSError {
      // handle error
    }
   ```
   {: codeblock}
   {: ios}

1. Download the native iOS Swift application project from the **Samples** section. The project contains a native iOS Swift application that uses the JSONStore API set. JavaScript adapter Maven project can be downloaded from [here](https://github.com/MobileFirst-Platform-Developer-Center/JSONStoreAdapter/tree/release80).
{: ios}

Adapter integration is optional and provides ways to send data from a collection to an adapter and get data from an adapter into a collection.
You can achieve these goals by using functions such as `WLResourceRequest` or your own instance of an `HttpClient` if you need more flexibility.
{: android}

1. Create an adapter and name it **JSONStoreAdapter**.
1. Define its procedures `addPerson`, `getPeople`, `pushPeople`, `removePerson`, and `replacePerson`.
1. To load data from an adapter use `WLResourceRequest`.

   ```java
    WLResponseListener responseListener = new WLResponseListener() {
      @Override
      public void onFailure(final WLFailResponse response) {
        // handle failure
      }
      @Override
      public void onSuccess(WLResponse response) {
        try {
          JSONArray loadedDocuments = response.getResponseJSON().getJSONArray("peopleList");
        } catch(Exception e) {
          // error decoding JSON data
        }
      }
    };

    try {
      WLResourceRequest request = new WLResourceRequest(new URI("/adapters/JSONStoreAdapter/getPeople"), WLResourceRequest.GET);
      request.send(responseListener);
    } catch (URISyntaxException e) {
      // handle error
    }
   ```
   {: codeblock}
   {: android}

1. Calling `findAllDirtyDocuments` returns an array of so called "dirty documents", which are documents that have local modifications that don’t exist on the back-end system.

   ```java
    Context  context = getContext();
    try {
      String collectionName = "people";
      JSONStoreCollection collection = WLJSONStore.getInstance(context).getCollectionByName(collectionName);
      List<JSONObject> dirtyDocs = collection.findAllDirtyDocuments();
      // handle success
    } catch(JSONStoreException e) {
      // handle failure
    }
   ```
   {: codeblock}
   {: android}

   To prevent JSONStore from marking the documents as "dirty", pass the option `options.setMarkDirty(false)` to `add`, `replace`, and `remove`.
   {: tip}
   {: android}

1. To push changes to an adapter, call the `findAllDirtyDocuments` to get a list of documents with modifications and then use `WLResourceRequest`. After the data is sent and a successful response is received make sure, you call `markDocumentsClean`.

   ```java
    WLResponseListener responseListener = new WLResponseListener() {
      @Override
      public void onFailure(final WLFailResponse response) {
        // handle failure
      }
      @Override
      public void onSuccess(WLResponse response) {
        // handle success
      }
    };
    Context context = getContext();

    try {
      String collectionName = "people";
      JSONStoreCollection collection = WLJSONStore.getInstance(context).getCollectionByName(collectionName);
      List<JSONObject> dirtyDocuments = people.findAllDirtyDocuments();

      JSONObject payload = new JSONObject();
      payload.put("people", dirtyDocuments);

      WLResourceRequest request = new WLResourceRequest(new URI("/adapters/JSONStoreAdapter/pushPeople"), WLResourceRequest.POST);
      request.send(payload, responseListener);
    } catch(JSONStoreException e) {
      // handle failure
    } catch (URISyntaxException e) {
      // handle error
    }
   ```
   {: codeblock}
   {: android}

1. Download the native Android application project from the **Samples** section. The project contains a native Android application that uses the JSONStore API set. JavaScript adapter Maven project can be downloaded from [here](https://github.com/MobileFirst-Platform-Developer-Center/JSONStoreAdapter/tree/release80).
{: android}
