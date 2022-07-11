## Contents on this page:
- [Class Table](https://github.com/GodotNuts/GodotFirebase/wiki/Cloud-Functions#class-table)
- [Execute a Cloud function](https://github.com/GodotNuts/GodotFirebase/wiki/Cloud-Functions#execute-a-function)

***
# Class Table

|Class|Description|
|-|-|
|[`FirebaseFunctions`](https://github.com/GodotNuts/GodotFirebase/wiki/Cloud-Functions#FirebaseFunctions)|Cloud Functions module, lets user execute cloud function through Rest API interface.|
|[`FunctionTask`](https://github.com/GodotNuts/GodotFirebase/wiki/Cloud-Functions#FunctionTask)|Result of any request issued through Cloud Functions. Processes the request, emits signals and returns a result.|

<br/>

***


## Functions
> Firebase.Functions

|Functions|Description|
|-|-|
|`execute(function : String, method: int, params: Dictionary = {}, body: Dictionary = {}) -> FunctionTask`|Executes a function with name `function`, using HTTP method `method`, with parameters `params`; if needed, can pass a body as well. Returns a FunctionTask.|
<br/>

|Properties|Description|
|-|-|
|`persistence_enabled : bool`|Defaults to true and attempts to optimize results through caching. Despite defaulting to true, we recommend turning it off for now, as it's purely experimental for now.|
<br/>

|Signals|Description|
|-|-|
|`task_error(code : int, status : int, message : String)`|Emitted when a `function` execution request is not processed successfully by a `FunctionTask`.|
<br/>
***

## FunctionsTask
> returned by a Function execution request

|Functions|Description|
|-|-|
|||
<br/>

|Properties|Description|
|-|-|
|`data : Variant`|Contains the returned result of a processed Task.|
<br/>

|Signals|Description|
|-|-|
|`task_finished(result : Variant)`|Emitted when a Task has been processed. Returns the result of the request as a parameter. This is a lower level of signal communication between FunctionTasks, the inner Functions system, and your application.|
|`function_executed(response : int, result : String)`|Emitted when the `execute()` request is processed successfully; generally, you should listen to this and the task_error signal to ensure you are getting all possible outcomes. Result is probably a json string.|
|`task_error(code : int, status : int, data : String)`|Emitted when a Function `execute()` request is not processed successfully.|
<br/>
***

<p align="right"><a href="#contents-on-this-page">Back</a></p>
  
***  

## Executing a function
> Notes: you must be authenticated for this to work, and further you must have a given cloud function defined in Firebase; this wiki does not supply instructions for how to do that - see https://firebase.google.com/docs/functions for more.
```gdscript
Firebase.Functions.connect("task_error", self, "_on_task_error")

...

var task = Firebase.Functions.execute("MyFunctionName", HTTPClient.METHOD_POST, {}, { "user_id": Firebase.Auth.auth.local_id })
var result_dict = yield(task, "function_executed")
var user_info = MyUserInfo.new(result_dict.result) # Parse json into own user info object
```

<p align="right"><a href="#contents-on-this-page">Back</a></p> 

***

## Turn Off Local Cache
If you need to disable the local cache of the Firebase Plugin, you will need to change the following line in the `functions.gd` file to false

`addons > godot-firebase > functions > functions.gd`

```gdscript
var persistence_enabled : bool = false
```

<p align="right"><a href="#contents-on-this-page">Back</a></p> 

***

<p align="right"><a href="#contents-on-this-page">Back</a></p> 