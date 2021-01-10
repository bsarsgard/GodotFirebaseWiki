> You can query the Firebase Auth backend through a REST API. This can be used for various operations such as creating new users, signing in existing ones and editing or deleting these users.  
This plugin offers several methods to call these APIs just with one line of code.

## Contents on this page:
- [Signup with Email](https://github.com/WolfgangSenff/GodotFirebase/wiki/Authentication-and-User-Management#signup-with-email)
- [Login with Email](https://github.com/WolfgangSenff/GodotFirebase/wiki/Authentication-and-User-Management#login-with-email)
- [Examples](https://github.com/WolfgangSenff/GodotFirebase/wiki/Authentication-and-User-Management#examples)

***


## Signup with Email
```
Firebase.Auth.signup_with_email(email, password)
```

This will create the login_request_body variable and insert the correct data into it.

```python
var login_request_body = {
    "email":"",
    "password":"",
    "returnSecureToken": true
   }
```

From there the script will POST the data to the `signup_request_url` and add the user to the application  
<p align="right"><a href="#contents-on-this-page">Back</a></p>  


***
## Login with Email
```
Firebase.Auth.login_with_email(email, password)
```

This will create the login_request_body variable and insert the correct data into it.

```python
var login_request_body = {
    "email":"",
    "password":"",
    "returnSecureToken": true
   }
```

From there the script will POST the data to the `signin_request_url`, and wait for a response. The function `func _on_FirebaseAuth_request_completed(result, response_code, headers, body)` will take that response and parse it out for you.

#### Unable to parse body
If the script is unable to parse the body, it will print our an error to the console and 'return' out of the function

#### Body has RESPONSE_SIGNIN, RESPONSE_SIGNUP
If the response body has `RESPONSE_SIGNIN, RESPONSE_SIGNUP`, the user will be logged in and the refresh countdown will start
This refresh is needed for Firebase, as there is a limit to how long a connection can be left open, and you need the connection to stay open for updates

#### Body has RESPONSE_USERDATA
If the response body has `RESPONSE_USERDATA`, the script will emit a signal "userdata_received" with the userdata

#### Body has INVALID_EMAIL, EMAIL_NOT_FOUND, INVALID_PASSWORD, USER_DISABLED or WEAK_PASSWORD
If the response body has `INVALID_EMAIL, EMAIL_NOT_FOUND, INVALID_PASSWORD, USER_DISABLED or WEAK_PASSWORD`, the login has failed and the script will emit a signal "login_failed". It will also pass the error code and error message to be printed into the console
<p align="right"><a href="#contents-on-this-page">Back</a></p> 

***
### Verify User Account
```
Firebase.Auth.send_account_verification_email()
```

This function is used to send an account verification to an email associated with an ID. This will auto generate the account_verification_body and insert the correct data. This is best used after the user registers their account.

```python
var account_verification_body = {
	"requestType":"verify_email",
	"idToken":"",
   }
```

From there the script will POST the data to the `oobcode_request_url`, and wait for a response. The email associated with the ID will receive an email with a link to verify their account.

***
### Change User Email
```
Firebase.Auth.change_user_email(email)
```

This function is used to change the email address associated with the currently logged in user account. This function generates the change_email_body and inserts the correct data.

```python
var change_email_body = {
	"idToken":"",
	"email":"",
	"returnSecureToken": true,
   }
```

From there the script will post the data to the 'update_account_request_url', and wait for a response. The email for the associated user will then be updated in Firebase. Note that this function is for a user to change their own email, an admin can edit the email with the Web GUI.

***
### Change User Email
```
Firebase.Auth.change_user_password(password)
```

This function is used to change the password associated with the currently logged in user account. This function generates the change_password_body and inserts the correct data.

```python
var change_password_body = {
	"idToken":"",
	"password":"",
	"returnSecureToken": true,
   }
```

From there the script will post the data to the 'update_account_request_url', and wait for a response. The password for the associated user will then be updated in Firebase. Note that this function is for a user to change their own password.

***
## Examples

![signup login page](https://github.com/WolfgangSenff/GodotFirebase/wiki/images/signup_login_page.png)
```python
extends Node2D

func _ready():
	Firebase.Auth.connect("login_succeeded", self, "_on_FirebaseAuth_login_succeeded")
	Firebase.Auth.connect("login_failed", self, "on_login_failed")

func _on_login_pressed():
	var email = $email.text
	var password = $password.text
	Firebase.Auth.login_with_email_and_password(email, password)

func _on_register_pressed():
	var email = $email.text
	var password = $password.text
	Firebase.Auth.signup_with_email_and_password(email, password)

func _on_FirebaseAuth_login_succeeded(auth):
	var user = Firebase.Auth.get_user_data()
	print(user)
    
func on_login_failed(error_code, message):
	print("error code: " + str(error_code))
	print("message: " + str(message))
```
<p align="right"><a href="#contents-on-this-page">Back</a></p>  


***