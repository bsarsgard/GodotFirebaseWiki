> Firebase Dynamic Links allow you to generate shortlinks directly from your application

## Contents on this page:


## Generate A Link

```gdscript
generate_dynamic_link(long_link : String, APN : String, IBI : String, is_unguessable : bool)
```

* long_link -> The link you are trying to shorten
* APN -> Android Package Name (The app you want Android to open it with, defaults to web browser)
* IBI -> iOS Bundle ID (The app you want iOS to open it with, defaults to web browser)
* is_unguessable -> Such strings are created by base62-encoding randomly generated 96-bit numbers, and consist of 17 alphanumeric characters. Use unguessable strings to prevent your Dynamic Links from being crawled, which can potentially expose sensitive information.