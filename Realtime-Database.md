The Realtime Database functionality includes dynamic updates via the server-sent events protocol as implemented by Firebase. As such, database updates can happen and everyone connected to any path that's updated will be updated directly *without* the need to do a get at that path. This will store the data automatically for you as well and send a signal with the latest info.


## Contents on this page:
- [Connecting to a Path](https://github.com/GodotNuts/GodotFirebase/wiki/Realtime-Database#Connecting)
- [Filter](https://github.com/GodotNuts/GodotFirebase/wiki/Realtime-Database#Filter)

***
## Database
> Firebase.Database

|Functions|Description|
|-|-|
|`get_database_reference(path : String, filter : Dictionary) -> FirebaseDatabaseReference`||

Create a reference to a specific path inside the Realtime Database.
<br/>

## FirebaseDatabaseReference
> FirebaseDatabaseReference

|Signals|Description|
|-|-|
|`new_data_update(data)`|Emitted when new data is added to the path.|
|`patch_data_update(data)`|Emitted when data is updated within the path.|
|`push_successful()`|Emitted when data has been successfully pushed to the path.|
|`push_failed()`|Emitted when a request to push data to the path has failed.|
<br/>
***

## Connecting
> Note you need to be authenticated for this to work

The below will get you a basic reference to a path in the database; this will be updated automatically as the path is updated in the realtime database.

```gdscript
var db_ref = Firebase.Database.get_database_reference("path_to_position_in_database", {})
```

## Filter
> Note you need to be authenticated for this to work

The below will get you a filtered database reference to a path in your database. Note the constants supported for filtering are contained in Firebase.Database, near the top of the file.

```gdscript
var db_ref = Firebase.Database.get_database_reference("path_to_position_in_database", { Firebase.Database.LIMIT_TO_LAST : 10 })
```
