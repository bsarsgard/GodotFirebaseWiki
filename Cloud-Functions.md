## Contents on this page:
- [Class Table](https://github.com/GodotNuts/GodotFirebase/wiki/Cloud-Functions#class-table)
- [Deploy a Cloud Function](https://github.com/GodotNuts/GodotFirebase/wiki/Cloud-Functions#deploy-a-function)
- [Execute a Cloud function](https://github.com/GodotNuts/GodotFirebase/wiki/Cloud-Functions#execute-a-function)

***
# Class Table

|Class|Description|
|-|-|
|[`FirebaseFunctions`](https://github.com/GodotNuts/GodotFirebase/wiki/Cloud-Functions#FirebaseFunctions)|Cloud Functions module, lets user execute cloud function through Rest API interface.|
|[`FunctionTask`](https://github.com/GodotNuts/GodotFirebase/wiki/Cloud-Functions#FunctionTask)|Result of any request issued through Cloud Functions. Processes the request, emits signals and returns a result.|

<br/>

***


## Firestore
> Firebase.Firestore

|Functions|Description|
|-|-|
|`collection(collection_path : String) -> FirestoreCollection`|Create a reference to a collection inside Firestore. Returns a reference to a collection.|  
|`list(collection_path : String) -> FirestoreTask`|List all contents of a collection in Firestore.<br/>Returns a `FirestoreTask` issuing the request.|  
|`query(firestore_query : FirestoreQuery) -> FirestoreTask`|Issue a query on Firestore.<br/>Returns a `FirestoreTask` issuing the request.|  
<br/>

|Properties|Description|
|-|-|
|`collections : Dictionary`|A Dictionary containing all referenced collections.|  
|`auth : Dictionary`|A Dictionary containing all auth info for the current authenticated user.|  
<br/>

|Signals|Description|
|-|-|
|`listed_documents(documents : Array)`|Emitted when the `list()` request is processed successfully by a `FirestoreTask`.|
|`result_query(result : Array)`|Emitted when the `query()` request is processed successfully by a `FirestoreTask`.|
|`error(error : Dictionary)`|Emitted when a `query()` or `list()` request is not processed successfully by a `FirestoreTask`.|
<br/>
***

## FirestoreTask
> returned by a Firestore request

|Functions|Description|
|-|-|
|||
<br/>

|Properties|Description|
|-|-|
|`data : Variant`|Contains the result of a processed Task.|  
|`action : int`|Contains the action the task is processing or has processed.|
<br/>

|Signals|Description|
|-|-|
|`task_finished(result : Variant)`|Emitted when a Task has been processed. Returns the result of the request as a parameter. This is a lower level of signal communication between FirestoreTasks, Firestore and your application.|
|`listed_documents(documents : Array)`|Emitted when the `list()` request is processed successfully.|
|`result_query(result : Array)`|Emitted when the `query()` request is processed successfully.|
|`error(error : Dictionary)`|Emitted when a `query()` or `list()` request is not processed successfully.|
|`add_document(document_added : FirestoreDocument)`|Emitted when the `add()` request is processed.|
|`update_document(document_updated : FirestoreDocument)`|Emitted when the `update()` request is processed.|
|`get_document(document_got : FirestoreDocument)`|Emitted when the `get()` request is processed.|
|`delete_document()`|Emitted when the `delete()` request is processed.|
|`error(code, status, message)`|Emitted when a request has not processed correctly.|
<br/>
***

<p align="right"><a href="#contents-on-this-page">Back</a></p>
  
***  

## Connect To A Collection
> Note you need to be authenticated for this to work
```gdscript
Firebase.Firestore.collection('COLLECTION_NAME')
```
The following will return a collection from Firestore called `firestore_collection`. This collection can be called on later when adding or getting documents from it.
```gdscript
var firestore_collection : FirestoreCollection = Firebase.Firestore.collection('COLLECTION_NAME')
```

<p align="right"><a href="#contents-on-this-page">Back</a></p> 

***

## Turn Off Local Cache
If you need to disable the local cache of the Firebase Plugin, you will need to change the following line in the `firestore.gd` file to false

`addons > godot-firebase > firestore > firestore.gd`

```gdscript
var persistence_enabled : bool = false
```

<p align="right"><a href="#contents-on-this-page">Back</a></p> 

***

<p align="right"><a href="#contents-on-this-page">Back</a></p> 