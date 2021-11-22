## Contents on this page:
* [Installation of CLI](#install-the-firebase-cli)
* [Login and Test](#login-and-test)
* [Init and Deploy]($init-and-deploy)

## Install the Firebase CLI
The first thing you will need to do is install the [Firebase CLI](https://firebase.google.com/docs/cli) which will be used in the following steps. The Firebase CLI can be found at [https://firebase.google.com/docs/cli](https://firebase.google.com/docs/cli)

## Login and Test
You will need to login to Firebase to be able to work with your project. Please follow these steps

1. Run the following command
```powershell
firebase login
```

2. Once logged in, confirm access to projects with the following command
```powershell
firebase projects:list
``` 

## Init and Deploy

1. Create the directory where the project will be stored and then run the following command. This will walk you through all the features you would like installed
```powershell
firebase init
```

2. Once the directory is created and Firebase has been setup, you can copy all files into the `Public` folder
3. To deploy to Firebase Hosting run the following command
```powershell
firebase deploy
```

4. Optionally you can also run the following command to attach a commit message to it
```powershell
firebase deploy -m "Super Secret Message Goes Here"
```