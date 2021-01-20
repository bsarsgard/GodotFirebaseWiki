## Contents on this page:
- [Connect To A Collection](https://github.com/WolfgangSenff/GodotFirebase/wiki/Firestore#connect-to-a-collection)
- [Get A Document](https://github.com/WolfgangSenff/GodotFirebase/wiki/Firestore#get-a-document)
- [Add A Document](https://github.com/WolfgangSenff/GodotFirebase/wiki/Firestore#add-a-document)
- [Debugging](https://github.com/WolfgangSenff/GodotFirebase/wiki/Firestore#debugging)
- [Common Errors](https://github.com/WolfgangSenff/GodotFirebase/wiki/Firestore#common-errors)

***

## Connect To A Collection
> Note you need to be authenticated for this to work
```
Firebase.Firestore.collection('COLLECTION_NAME')
```
The following will return a collection from Firestore called `firestore_collection`. This collection can be called on later when adding or getting documents from it.
```
firestore_collection = Firebase.Firestore.collection('COLLECTION_NAME')
```

<p align="right"><a href="#contents-on-this-page">Back</a></p> 

***

## Get A Document
> Note you need to be authenticated and connected to a collection for this to work
```
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

The following will parse the data into a human readable format by using the function `fields2dict`

```
print(firestore_document.fields2dict(firestore_document.document))
```
Alternatively, a direct print will return the same result. The parsing will be done internally.
```
print(firestore_document)
```

<p align="right"><a href="#contents-on-this-page">Back</a></p> 

***

## Add A Document
> Note you need to be authenticated and connected to a collection for this to work
```
.add(documentId : String, fields : Dictionary = {})
```

The following will add a new document into Firestore by first creating the object, and then adding it. The function `dict2fields` is used to convert the dictionary of fields into the correct format for Firestore to use.


```
firestore_document : FirestoreDocument = FirestoreDocument.new()
firestore_collection.add("DOCUMENT_ID", firestore_document.dict2fields({'name': 'Document Name', 'active': 'true'}))
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