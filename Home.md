# Welcome to the GodotFirebase wiki!

Here you will find all the documentation on how to use this Godot Firebase Plugin.

If you are unsure where to start, check out the following pages:

* [Installation and Activation](https://github.com/WolfgangSenff/GodotFirebase/wiki/Installation-and-Activation)
* [Authentication and User Management](https://github.com/WolfgangSenff/GodotFirebase/wiki/Authentication-and-User-Management)
* Demos and Getting Started

## Design
This plugin is designed around the Firebase REST API. This means it is massively cross-platform, far more than any other Firebase plugin or library, because they have code that is (generally) Android- or iOS-only. Since it's a Godot plugin, it also does not require recompiling the Godot with an additional module whenever an updated version is released. It is verified to work across all of the following platforms at present:

## Supported platforms
* Android
* iOS
* Mac
* Windows
* Linux
* Serverless
* UWP

At the moment, there appears to be a bug with HTML5 export, but the team will be verifying/debugging it in the near future.

## Supported features
* Realtime Database
* Firestore
* Authentication and User Management

## Unsupported features
* Dynamic Links - Link Shortener (in progress)
* Analytics - no real REST API at the moment
* Storage - preliminary investigations have begun
* Offline support - preliminary investigations have begun
* Remote Config - preliminary investigations have begun