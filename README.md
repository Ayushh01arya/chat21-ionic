[![npm version](https://badge.fury.io/js/%40chat21%2Fchat21-ionic.svg)](https://badge.fury.io/js/%40chat21%2Fchat21-ionic)

Chat21 is the core of the open source live chat platform [Tiledesk.com](http://www.tiledesk.com).

# Features #
With Chat21-ionic you can:
* Send a direct message to a user (one to one message)
* View the messages history
* The read receipts feature allows your users to see when a message has been sent, delivered and read
* Conversations list view with the last messages sent (like Whatsapp)
* With the Presense Manager you can view when a user is online or offline and the inactivity period
* Responsive design (desktop and mobile)
* View the user profile with fullname and email 
* Login with email and password (Use firebase email and password authentication method )
* Signup  with fullname, email, password and profile picture
* Contacts list view with fulltext search for fullname field

# Live Demo #
Visit https://web.chat21.org/ to see a live demo of chat21-ionic.

<img src="https://user-images.githubusercontent.com/9556761/57692753-df24d780-7647-11e9-9505-82ee5288637c.png" alt="A screenshot of chat21-ionic demo" style="max-width:100%;">

<img src="https://user-images.githubusercontent.com/9556761/57692765-e3e98b80-7647-11e9-8afe-b21e6085d7ca.png" alt="A screenshot of chat21-ionic demo" style="max-width:100%;">

# Documentation #
In progress

# Prerequisites #
* Install nodejs: `https://nodejs.org/en/download/`
* Install git: `https://git-scm.com/book/id/v2/Getting-Started-Installing-Git`
* Install Ionic CLI and Cordova : `https://ionicframework.com/docs/intro/installation/`
* A Firebase project. Create one free on `https://firebase.google.com`
* "Chat21 Firebase cloud functions" installed. Instructions:`https://github.com/chat21/chat21-cloud-functions`

# Installation #
* Clone this repository. Run: `git clone https://github.com/frontiere21/chat21-ionic.git` in the folder in which you'd like to contain the project.
* Build running: `npm install`

# Firebase 
* Create account Firebase
* Create a Firebase project in the Firebase console, if you don't already have one. https://console.firebase.google.com/
* Deploy Chat21 Firebase Cloud Functions as described here: https://github.com/chat21/chat21-cloud-functions

## Configuration ## 
* Configure the file environment.ts in src/environments folder:     
    ```
    export const environment = {
     production: false,
     remoteConfig: false,
     remoteConfigUrl: '/firebase-config.json',
     firebaseConfig : {
        apiKey: 'CHANGEIT',
        authDomain: 'CHANGEIT',
        databaseURL: 'CHANGEIT',
        projectId: 'CHANGEIT',
        storageBucket: 'CHANGEIT',
        messagingSenderId: 'CHANGEIT',
        chat21ApiUrl: 'CHANGEIT'
    }
  };```
  

* (optional) Update app.module.ts: 
    * open `/src/app/app.module.ts` and change tenant name
* Update app constants in `src/utils/constants.ts`

### Push notification
* open `/src/firebase-messaging-sw.js` and replace messagingSenderId: with < your messagingSenderId >
More info here :  https://angularfirebase.com/lessons/send-push-notifications-in-angular-with-firebase-cloud-messaging/
* firebase-messaging-sw.js must be accessible in the root of your  without context for example (https://support.tiledesk.com/firebase-messaging-sw.js)
* After the build process check the property gcm_sender_id of the manifest.json file. The correct value for firebase is:
`"gcm_sender_id": "103953800507"`
    
### (Optional) Authenticate with email password  
* Config Firebase auth
In the Firebase Console open the Authentication section > SIGN IN METHOD tab you need to enable the Email/password Sign-in Provider and click SAVE. This will allow users to sign-in the Web app with their Email
https://firebase.google.com/docs/auth/

## Run App on Browser ##
* Now you will need to serve the app. Run: `ionic serve` in the terminal. (Update the plugins if required)

## Create build browser ##
* Run: `cordova platform add browser@latest`
* Run: `ionic cordova build browser`

# Deploy
## Deploy on a WebServer (Apache or Nginx)
Copy the content of the directory platforms/browser/www to your WebServer public dir.

## Deploy on firebase hosting ##
https://firebase.google.com/docs/hosting/quickstart?authuser=0
* Install the Firebase CLI. run: `npm install -g firebase-tools`
* Run: `firebase login`
(these steps can be avoided if you have already done before)
* Change directories in the terminal to your desired project directory(run: `cd platforms/browser`) and run: `firebase init`
    * select hosting (press Spacebar to select) and press return
    * select your project and press return
    * answer the following questions:
        * "what do you want to use as your public directory?"  www and press return  
        * "configure as a single-page app?"  N and press return
        * "file www/index.html alredy exists. Overwrite?" N and press return
* Run: `firebase deploy`
* In your firebase consol click hosting and click on link your project

## Run on Android and iOS
* Run on simulator : `ionic cordova run android`
* Run on device : `ionic cordova run android --device`

* Run on simulator : `ionic cordova run ios`
* Run on device : `ionic cordova run ios --device`
