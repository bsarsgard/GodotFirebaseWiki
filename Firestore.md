## Contents on this page:
- [Connect To A Collection](https://github.com/WolfgangSenff/GodotFirebase/wiki/Firestore#connect-to-a-collection)
- [Get A Document](https://github.com/WolfgangSenff/GodotFirebase/wiki/Firestore#get-a-document)
- [Add A Document](https://github.com/WolfgangSenff/GodotFirebase/wiki/Firestore#add-a-document)
- [Debugging](https://github.com/WolfgangSenff/GodotFirebase/wiki/Firestore#debugging)
- [Common Errors](https://github.com/WolfgangSenff/GodotFirebase/wiki/Firestore#common-errors)

***
## Firestore
> Firebase.Firestore

|Functions|Description|
|-|-|
|`collection(collection_path : String) -> FirestoreCollection`|Create a reference to a collection inside Firestore.|  
|`list(collection_path : String) -> void`|List all contents of a path in Firestore.|  
<br/>

|Properties|Description|
|-|-|
|`collections : Dictionary`|A Dictionary containing all referenced collections.|  
|`auth : Dictionary`|A Dictionary containing all auth info for the current authenticated user.|  
<br/>

|Signals|Description|
|-|-|
|`listed_documents(documents)`|Emitted when the `list()` request is processed.|
<br/>

## FirestoreCollection
> Firebase.Firestore.collection()

|Functions|Description|
|-|-|
|`add(document_id : String, fields : Dictionary) -> void`|Add a Document to a Collection. If `document_id` is left to `""` the id will be randomically given by Firebase.|  
|`update(document_id : String, fields : Dictionary) -> void`|Update a specified Document to a Collection. If `document_id` is left to `""` the id will be randomically given by Firebase, creating a new Document. If the document with the given `document_id` does not exist, it will be created.|  
|`get(document_id : String) -> void`|Get a specific Document.|  
|`delete(document_id : String) -> void`|Delete a specific Document.|  
<br/>

|Properties|Description|
|-|-|
|`base_url : String`||  
|`extended_url : String`||  
|`collection_name : String`||  
<br/>

|Signals|Description|
|-|-|
|`add_document(document_added : FirestoreDocument)`|Emitted when the `add()` request is processed.|
|`update_document(document_updated : FirestoreDocument)`|Emitted when the `update()` request is processed.|
|`get_document(document_got : FirestoreDocument)`|Emitted when the `get()` request is processed.|
|`delete_document()`|Emitted when the `delete()` request is processed.|
|`error(code, status, message)`|Emitted when a request has not processed correctly.|
<br/>

## FirestoreDocument
> FirestoreDocument.new() or from a signal

|Functions|Description|
|-|-|
|`static dict2fields(dictionary : Dictionary) -> Dictionary`|Parse a GDScript Dictionary to a Firebase dictionary of fields.|  
|`static fields2dict(fields : Dictionary) -> Dictionary`|Parse a Firebase dictionary of fields to a GDScript Dictionary.|  
|`_to_string()`|Automatically called on `print(document) to print a formatted document.`|
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

## Connect To A Collection
> Note you need to be authenticated for this to work
```gdscript
Firebase.Firestore.collection('COLLECTION_NAME')
```
The following will return a collection from Firestore called `firestore_collection`. This collection can be called on later when adding or getting documents from it.
```gdscript
firestore_collection = Firebase.Firestore.collection('COLLECTION_NAME')
```

<p align="right"><a href="#contents-on-this-page">Back</a></p> 

***

## Get A Document
> Note you need to be authenticated and connected to a collection for this to work
```gdscript
.get(documentId : String)
```

**Note:** Unlike collections (which is just a reference) this function won't return directly a real document, but will request the specified document which will be returned with a signal.  
The following methods will let you return a document from Firestore with the `DOCUMENT_ID` that is specified to an object called `firestore_document`: 
1. Call the `.get()` function and than yield for the collection to return it with a signal
```gdscript
var collection : FirestoreCollection = Firebase.Firestore.collection(COLLECTION_ID)
collection.get(DOCUMENT_ID)
var document : FirestoreDocument = yield(collection, "get_document")
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

```
print(firestore_document)
```


<p align="right"><a href="#contents-on-this-page">Back</a></p> 

***

## Add A Document
> Note you need to be authenticated and connected to a collection for this to work
```gdscript
.add(documentId : String, fields : Dictionary = {})
```

The following will add a new document into Firestore by first creating the object, and then adding it. 


```
firestore_collection.add("DOCUMENT_ID", {'name': 'Document Name', 'active': 'true'})
```

Internally, the `FirestoreCollection` instance will call the `dict2fields()` , used to convert the dictionary of fields into the correct format for Firestore to use.
> Note: if "DOCUMENT_ID" is left as an empty String like `""` Firebase will assign to this document a random name. This name will be returned through FirestoreCollection signals.

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

```
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