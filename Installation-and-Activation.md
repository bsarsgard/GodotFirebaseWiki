## Installation
1. Install this plugin:
	1. [**recommended**] Copy this repository and extract all of the `GodotFirebase-main` contents (`addons/` folder including `.env` file) to the root of your project at `res://`  
	*--- or ---*
	2. [**not recommended - always check version**] Install this addon from the AssetLibrary inside Godot Engine's Editor: go to the `AssetLib` panel on the top bar and look for `GodotFirebase`. When choosing which folders to install, **only check `addons/` folder and `override.cfg` file**
2. Open your Project Settings
3. Go to Plugins
4. Activate the GDFirebase plugin<br>
![Plugin Section](https://github.com/WolfgangSenff/GodotFirebase/wiki/images/plugins_section.png)
5. From there, you will have an autoload singleton with the variables Auth and Database. Reference it by using Firebase.Auth, etc.

## Activation

1. Go create a Firebase app at console.firebase.google.com. A Guide can be found [Here](https://firebase.google.com/docs/projects/learn-more#setting_up_a_firebase_project_and_connecting_apps)

2. Once the app has been created, add a web app to it:

    1. Click on the **Project Settings** option<br>
    ![FB Project Settings](https://github.com/WolfgangSenff/GodotFirebase/wiki/images/fb_project_settings.png)

    2. Click on the **Add App** button<br>
    ![FB Add App](https://github.com/WolfgangSenff/GodotFirebase/wiki/images/fb_add_app.png)

    3. Click the **Web App** button<br>
    ![FB Web App](https://github.com/WolfgangSenff/GodotFirebase/wiki/images/fb_web_app.png)

    4. Add a name to your web app and click **Register App**<br>
    ![FB Register App](https://github.com/WolfgangSenff/GodotFirebase/wiki/images/fb_register_app.png)

3. This will show a series of values called "config". To use them you have two options:

    1. Take those values and copy them to the appropriate variables in `res://addons/godot-firebase/firebase.gd`.

    2. (Recommended) Create a `.env` file at the root of the GodotFirebase plugin (specifically, `res://addons/godot-firebase/.env`). Specify those values as environment variables in this file (see example structure below). Reload the project, and you will find a new category inside `Project ↝ Project Settings ↝ General ↝ Firebase`, which is `Environment Variables`. Fill all the fields inside this new category and you will be good to go. 

```
[firebase/environment_variables]

apiKey=""
authDomain=""
databaseURL=""
projectId=""
storageBucket=""
messagingSenderId=""
appId=""
measurementId=""
clientId=""
clientSecret=""
domainUriPrefix=""
```

## (Additional) OAuth configuration
In order to let users login with their own Google account to your app, the OAuth authentication process must be configured to work with this Plugin.  
This process will not be enabled with the main configuration, but still it is *not mandatory* to use standard login methods.  
To enable Google OAuth Authentication, follow these steps:
1. In your project, enable "Google" in "Sign-in Method":
![enable_sign_in](./images/OAuth/sign.png)
2. Go to [console.cloud.google.com/apis/credentials](https://console.cloud.google.com/apis/credentials):
![go_to](./images/OAuth/browser.png)
3. Select the project you are working on (and eventually, your organization):
![select_project](./images/OAuth/project.gif)
4. Press the "+ Create Credentials" button and chose "ID Client OAuth" to register new credentials:
![create_credentials](./images/OAuth/id.png)
5. Select **Desktop Application**, then give a name to your credentials:
![desktop](./images/OAuth/type.png)
6. Create your credentials and copy-paste them in the configuration file `.env`, or directly in your code:
![keys](./images/OAuth/keys.png)
![config](./images/OAuth/config.png)
