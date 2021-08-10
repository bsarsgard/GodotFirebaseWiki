> Firebase Cloud Storage can be used for storing large amounts of data that your app may use, whether it's user specific, or accessed everywhere.
> This plugin's storage API allows you to access all this.

## Contents of this page:
* [Storage](https://github.com/GodotNuts/GodotFirebase/wiki/Storage#storage)
* [StorageReference](https://github.com/GodotNuts/GodotFirebase/wiki/Storage#storagereference)
* [StorageTask](https://github.com/GodotNuts/GodotFirebase/wiki/Storage#storagetask)

***

## Storage
> Firebase.Storage

This class is used globally, and is responsible for handling data requests between your app and your Firebase project.
| Functions | Descriptions |
|---|---|
|`ref(file_path :String) -> StorageReference`| Creates a reference to a file/folder in your cloud storage.|

## StorageReference
> StorageReference

These kinds of objects act as a reference to files and folders in your cloud storage. They have functions that allow you to interact with the server-side files.
| Properties | Descriptions |
|---|---|
|`bucket :String`| The bucket that this `StorageReference` is in.|
|`full_path :String`| The path of the file relative to the storage bucket.|
|`name :String`| The name of the file, including the extension.|
|`parent :StorageReference`| The parent of this `StorageReference`. If said `StorageReference` is the root, then the parent is `Null`.|
|`root :StorageReference`| The root of this `StorageReference`.|
|`storage :FirebaseStorage`| The global class that handles all http requests on behalf of the `StorageReference`.|
|`valid :bool`| Whether this `StorageReference` is valid. None of the functions will work when in an invalid state. Set to `false` when `delete()` is called.|

| Functions | Descriptions |
|---|---|
|`child(file_path :String) -> StorageReference`| Returns a reference relative to `file_path`.|
|`put_data(data :PoolByteArray, metadata := {}) -> StorageTask`| Uploads the raw `data` to storage, along with `metadata`. Returns a `StorageTask` to keep track of it.|
|`put_string(data :String, metadata := {}) -> StorageTask`| Like `put_data()`, but with a `String` instead of a raw array of bytes.|
|`put_file(file_path :String, metadata := {}) -> StorageTask`| Like `put_data()`, but with a `file_path` that will have it's referencing file data passed into storage.|
|`get_data() -> StorageTask`| Requests data from storage. The data will be placed inside the returned `StorageTask` in the form of a `PoolByteArray`.|
|`get_string() -> StorageTask`| Like `get_data()`, but the data will be in the form of a string.|
|`get_download_url() -> StorageTask`| Requests a URL that points to the file. The result will be stored inside the returned `StorageTask`.|
|`get_metadata() -> StorageTask`| Requests the file's metadata. The metadata will be stored inside the returned `StorageTask`.|
|`update_metadata(metadata :Dictionary) -> StorageTask`| Updates the file's metadata. Any entry that's null will be deleted from storage. Returns a `StorageTask` to keep track of it.|
|`list() -> StorageTask`| Requests the list of folders and/or files that is under the referenced folder. Said list will be inside the returned `StorageTask`.|
|`list_all() -> StorageTask`| Like `list()`, but includes any sub-folders' contents as well.|
|`delete() -> StorageTask`| Deletes the file from storage. Once done, this `StorageReference` will become invalid.|

## StorageTask
> StorageTask

These objects are used to keep track of any of `StorageReference's` function calls that involve uploading or downloading data from storage. They also contain they're returning data.
| Properties | Descriptions |
|---|---|
|`ref :StorageReference`| The reference that this `StorageTask` was created from.|
|`action :int`| The kind of task this `StorageTask` is tracking.|
|`data :Variant`| Data that the tracked task returns.|
|`progress :float`| Tracks the percentage of data that the tracked task has downloaded.|
|`result :int`| The status of the task once it's finished. Any number other than `0` is an error (See HTTPRequest.Result).|
|`finished :bool`| Whether the tracked task is finished.|
|`response_headers :PoolStringArray`| HTTP Response headers that the task finishes with.|
|`response_code :int`| HTTP Response code that the task finishes with.|

| Signals | Descriptions |
|---|---|
|`task_finished`| Emits when the tracked task is finished.|

| Enumerations | Descriptions |
|---|---|
|`TASK_UPLOAD`||
|`TASK_UPLOAD_META`||
|`TASK_DOWNLOAD`||
|`TASK_DOWNLOAD_META`||
|`TASK_DOWNLOAD_URL`||
|`TASK_LIST`||
|`TASK_LIST_ALL`||
|`TASK_DELETE`||
|`TASK_MAX`| This marks the amount of TASK enumerations.|

***

## Put File
```
Firebase.Storage.ref(storage refernce).put_file(local file)
```
[**Usage Example**](#ex-put-file)

This will upload a local file into Storage for later use

```python
var upload_task = Firebase.Storage.ref("Firebasetester/upload/icon.png").put_file("res://icon.png")
yield(upload_task, "task_finished")
```

***

## Put String
```
Firebase.Storage.ref(storage refernce).put_string(String, {metadata})
```
[**Usage Example**](#ex-put-string)

This will upload a string for later use

```python
upload_task = Firebase.Storage.ref("Firebasetester/upload/junkdata").put_string("Test", {})
yield(upload_task, "task_finished")
```

***

## Get Download URL
```
Firebase.Storage.ref(storage reference).get_download_url()
```
[**Usage Example**](#ex-get-download-url)

This will get the download URL and display it in the console

```python
var url_task = Firebase.Storage.ref("Firebasetester/upload/icon.png").get_download_url()
yield(url_task, "task_finished")
print(url_task.data)
```

***

## Get Metadata
```
Firebase.Storage.ref(storage reference).get_metadata()
```
[**Usage Example**](#ex-get-metadata)

This will get download the metadata for an object in storage and print it to the console

```python
var meta_task = Firebase.Storage.ref("Firebasetester/upload/icon.png").get_metadata()
yield(meta_task, "task_finished")
print(meta_task.data)
```

***

## Delete Object
```
Firebase.Storage.ref(storage reference).delete()
```
[**Usage Example**](#ex-delete-object)

This will delete an object in storage 

```python
var delete_task = Firebase.Storage.ref("Firebasetester/upload/icon.png").delete()
yield(delete_task, "task_finished")
```

***

## List All Objects
```
Firebase.Storage.ref(storage reference).list_all()
```
[**Usage Example**](#ex-list-objects)

This will list all objects in storage and print it to the console

```python
list_all_task = Firebase.Storage.ref("Firebasetester").list_all()
yield(list_all_task, "task_finished")
print(list_all_task.data)
```