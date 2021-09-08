## Contents on this page:
- [Class Table](https://github.com/GodotNuts/GodotFirebase/wiki/Firestore#class-table)
- [Connect To A Collection](https://github.com/GodotNuts/GodotFirebase/wiki/Firestore#connect-to-a-collection)
- [Turn Off Local Cache](https://github.com/GodotNuts/GodotFirebase/wiki/Firestore#turn-off-local-cache)
- [Get A Document](https://github.com/GodotNuts/GodotFirebase/wiki/Firestore#get-a-document)
- [Add A Document](https://github.com/GodotNuts/GodotFirebase/wiki/Firestore#add-a-document)
- [Update A Document](https://github.com/GodotNuts/GodotFirebase/wiki/Firestore#update-a-document)
- [Delete A Document](https://github.com/GodotNuts/GodotFirebase/wiki/Firestore#delete-a-document)
- [Issue a Query](https://github.com/GodotNuts/GodotFirebase/wiki/Firestore#issue-a-query)
- [Debugging](https://github.com/GodotNuts/GodotFirebase/wiki/Firestore#debugging)
- [Common Errors](https://github.com/GodotNuts/GodotFirebase/wiki/Firestore#common-errors)

***
# Class Table

|Class|Description|
|-|-|
|[`Firestore`](https://github.com/GodotNuts/GodotFirebase/wiki/Firestore#firestore)|Firestore module, lets user connect to collections, issue queries and request a list of documents/collections at a specified path.|
|[`FirestoreCollection`](https://github.com/GodotNuts/GodotFirebase/wiki/Firestore#firestorecollection)|A reference to a colleciton in Firestore, used to call functions to manage documents or nested collections.|
|[`FirestoreDocument`](https://github.com/GodotNuts/GodotFirebase/wiki/Firestore#firestoredocument)|An object representing a fetched, updated or deleted document in Firestore.|
|[`FirestoreTask`](https://github.com/GodotNuts/GodotFirebase/wiki/Firestore#firestoretask)|Result of any request issued through Firestore. Processes the request, emits signals and returns a result.|
|[`FirestoreQuery`](https://github.com/GodotNuts/GodotFirebase/wiki/Firestore#firestorequery)|An object representing a query to Firestore, used as a parameter for the `query()` function.|

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

## FirestoreCollection
> Firebase.Firestore.collection()

|Functions &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |Description|
|---------|-|
|`add(document_id : String, fields : Dictionary) -> FirestoreTask`|Add a Document to a Collection.<br/>If `document_id` is left to `""` the id will be randomically given by Firebase.|  
|`update(document_id : String, fields : Dictionary) -> FirestoreTask`|Update a specified Document to a Collection. If `document_id` is left to `""` the id will be randomically given by Firebase, creating a new Document.<br/>If the document with the given `document_id` does not exist, it will be created.|  
|`get(document_id : String) -> FirestoreTask`|Get a specific Document.|  
|`delete(document_id : String) -> FirestoreTask`|Delete a specific Document.|  
<br/>

|Properties|Description|
|-|-|
|`config : Dictionary`|Configuration settings for this plugin.|  
|`auth : Dictionary`|Authentication dictionary to issue requests as a logged user.|  
|`collection_name : String`|The referenced collection's name|  
<br/>

|Signals|Description|
|-|-|
|`add_document(document_added : FirestoreDocument)`|Emitted when the `add()` request is processed by a `FirestoreTask`.|
|`update_document(document_updated : FirestoreDocument)`|Emitted when the `update()` request is processed by a `FirestoreTask`.|
|`get_document(document_got : FirestoreDocument)`|Emitted when the `get()` request is processed by a `FirestoreTask`.|
|`delete_document()`|Emitted when the `delete()` request is processed by a `FirestoreTask`.|
|`error(code, status, message)`|Emitted when a request has not processed correctly by a `FirestoreTask`.|

<br/>

***  

## FirestoreDocument
> FirestoreDocument.new() or from a signal

|Functions|Description|
|-|-|
|`static dict2fields(dictionary : Dictionary) -> Dictionary`|Parse a GDScript Dictionary to a Firebase dictionary of fields.|  
|`static fields2dict(fields : Dictionary) -> Dictionary`|Parse a Firebase dictionary of fields to a GDScript Dictionary.|  
|`_to_string() -> String`|Automatically called on `print(document)` to print a formatted document.|
<br/>

|Properties|Description|
|-|-|
|`doc_name : String`|The document name.|  
|`doc_fields : Dictionary`|The document fields, as a GDScript Dictionary.|
|`create_at : String`|Timestamp of creation date.|  
<br/>

|Signals|Description|
|-|-|
|||
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

## FirestoreQuery
> FirestoreQuery.new()

|Properties|Description|
|-|-|
|`doc_name : String`|The document name.|  
|`doc_fields : Dictionary`|The document fields, as a GDScript Dictionary.|
|`create_at : String`|Timestamp of creation date.|  
<br/>

|Functions|Description|
|-|-|
|`select(fields : Variant)`|A `SELECT` query on a Collection, `fields` can be an Arrat/PoolStringArray of fields, or just a String for a single field.|  
|`from(collection_id : String, all_descendants : bool = true)`|A `FROM` query to a single Collection.|  
|`from_many(collections : Array)`|A `FROM` query on multiple Collections. `collections` must be an Array of Arrays of type `[collection_id:String, all_descendants:bool]`.|  
|`where(field : String, operator : FirestoreQuery.OPERATOR, value : Variant, chain : int = -1)`|A `WHERE` query to match fields' values with Operators.<br/>`operator` must be a `FirestoreQuery.Operator` element.<br/>`chain` can be `OPERATOR.AND` or `OPERATOR.OR` to chain multiple `where()` in sequence. The last one in a chain (or if a single one) must have `chain = -1` (automatically injected).|
|`order_by(field : String, direction : int = DIRECTION.ASCENDING)`|A `ORDER BY` query on a Collection. Direction must be of type `FirestoreQuery.DIRECTION`.|
|`order_by_fields(order_field_list : Array)`|A `ORDER BY` query on a Collection based on multiple fields. `order_field_list` must be an Array of Arrays with structure `[field : String, order : DIRECTION]`.|
|`start_at(value : Variant, before : bool)`|A `START AT` query on a Collection. `value` can be of any type, define if you want to list values `before` or not the specified one.|
|`end_at(value : Variant, before : bool)`|A `END AT` query on a Collection. `value` can be of any type, define if you want to list values `before` or not the specified one.|
|`offset(offset : int)`|A `OFFSET` query on a Collection to define the amount of results to be skipped.|
|`limit(limit : int)`|A `LIMIT` query on a Collection to define the amount of results to be returned.|
<br/>  

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

## Get A Document
> Note you need to be authenticated and connected to a collection for this to work
```gdscript
.get(documentId : String) -> FirestoreTask
```

**Note:** Unlike collections (which is just a reference) this function won't return directly a real document, but will request the specified document which will be returned with a signal.  
The following methods will let you return a document from Firestore with the `DOCUMENT_ID` that is specified to an object called `firestore_document` of type `FirestoreDocument`: 
1. Call the `.get()` function and than yield for the collection to return it with a signal
```gdscript
var collection : FirestoreCollection = Firebase.Firestore.collection(COLLECTION_ID)
collection.get(DOCUMENT_ID)
var document : FirestoreDocument = yield(collection, "get_document")

- or -

var collection : FirestoreCollection = Firebase.Firestore.collection(COLLECTION_ID)
var document_task : FirestoreTask = collection.get(DOCUMENT_ID)
var document : FirestoreDocument = yield(document_task, "get_document")
```
2. Connect a signal to the collection and get the document separately
```gdscript
var collection : FirestoreCollection = Firebase.Firestore.collection(COLLECTION_ID)
collection.connect("get_document",self,"_on_get_document")
collection.get(DOCUMENT_ID)

[...]

func _on_get_document(document : FirestoreDocument) -> void:
	pass
``` 

The following will parse the data into a human readable format with automatic parsing, from Firebase format to Dictionary.

```gdscript
print(firestore_document)
```


<p align="right"><a href="#contents-on-this-page">Back</a></p> 

***

## Add A Document
> Note you need to be authenticated and connected to a collection for this to work
```gdscript
.add(documentId : String, fields : Dictionary = {}) -> FirestoreTask
```

The following will add a new document into Firestore by first creating the object, and then adding it. 


```gdscript
var add_task : FirestoreTask = firestore_collection.add("DOCUMENT_ID", {'name': 'Document Name', 'active': 'true'})
var document : FirestoreDocument = yield(add_task, "task_finished")

- or -

var document : FirestoreDocument = yield(add_task, "add_document")

- or -

var document : FirestoreDocument = yield(Firebase.Firestore, "add_document")
```

Internally, the `FirestoreCollection` instance will call the `dict2fields()` , used to convert the dictionary of fields into the correct format for Firestore to use.
> Note: if "DOCUMENT_ID" is left as an empty String like `""` Firebase will assign to this document a random name. This name will be returned through FirestoreCollection signals.

<p align="right"><a href="#contents-on-this-page">Back</a></p> 

***

## Update A Document
> Note you need to be authenticated and connected to a collection for this to work
```gdscript
.update(documentId : String, fields : Dictionary = {}) -> FirestoreTask
```

The following will update document in Firestore.


```gdscript
var up_task : FirestoreTask = firestore_collection.update("DOCUMENT_ID", {'name': 'Document Name', 'active': 'true'})
var document : FirestoreDocument = yield(up_task, "task_finished")

- or -

var document : FirestoreDocument = yield(up_task, "update_document")

- or -

var document : FirestoreDocument = yield(Firebase.Firestore, "update_document")
```

Internally, the `FirestoreCollection` instance will call the `dict2fields()` , used to convert the dictionary of fields into the correct format for Firestore to use.

<p align="right"><a href="#contents-on-this-page">Back</a></p> 

***

## Delete A Document
> Note you need to be authenticated and connected to a collection for this to work
```gdscript
.delete(documentId : String) -> FirestoreTask
```

The following will delete a new document in Firestore.
```gdscript
var del_task : FirestoreTask = firestore_collection.delete("DOCUMENT_ID")
var document : FirestoreDocument = yield(del_task, "task_finished")
```

<p align="right"><a href="#contents-on-this-page">Back</a></p> 

***

## Issue a Query
> Note you need to be authenticated for this to work
```gdscript
Firebase.Firestore.query(FirestoreQuery.new()) -> FirestoreTask
```

The following query some documents from a collection based on the value of a field. 


```gdscript
# create a query
var query : FirestoreQuery = FirestoreQuery.new()

# FROM a collection
query.from("user_list")	

# WHERE points > 20
query.where("points", FirestoreQuery.OPERATOR.GREATER_THAN, 20)

# ORDER BY points, from the user with the best score to the latest
query.order_by("points", FirestoreQuery.DIRECTION.DESCENDING)

# LIMIT to the first 10 users
query.limit(10)

# Issue the query
var query_task : FirestoreTask = Firebase.Firestore.query(query)

# Yield on the request to get a result
var result : Array = yield(query_task, "task_finished")
```

> Note: each FirestoreQuery function will always return itself, so queries component can be concatenated to create single-line queries

```gdscript
# Do all the previous, but in one line
var query : FirestoreQuery = FirestoreQuery.new().from("user_list").where("points", FirestoreQuery.OPERATOR.GREATER_THAN, 20).order_by("points", FirestoreQuery.DIRECTION.DESCENDING).limit(10)

var result : Array = yield(Firestore.Firebase.query(query), "result_query")
```
<p align="right"><a href="#contents-on-this-page">Back</a></p> 

***

## Debugging
> Note you need to be authenticated and connected to a collection for this to work

There are some signals that can be connected to for the purpose of debugging

- Signal ("add_document", document )
- Signal ("get_document", document )
- Signal ("update_document", document )
- Signal ("delete_document")
- Signal ("error",bod.error.code,bod.error.status,bod.error.message)

These signals need to be connected to from the collection

```gdscript
firestore_collection.connect("add_document", self, "on_document_add")
firestore_collection.connect("get_document", self, "on_document_get")
firestore_collection.connect("update_document", self, "on_document_update")
firestore_collection.connect("delete_document", self, "on_document_delete")
firestore_collection.connect("error", self, "on_document_error")
```

<p align="right"><a href="#contents-on-this-page">Back</a></p> 

***

## Common Errors

#### Unauthorized
This occurs when you are trying to do something with a collection but have not logged in

<p align="right"><a href="#contents-on-this-page">Back</a></p> 