<p align="center">
  <h2 align="center">React Native Firebase - Messaging</h2>
</p>

<p align="center">
  <a href="https://github.com/invertase/react-native-firebase/tree/master/packages/messaging">Original Documentation</a>
</p>

----

Original Android implementation uses a broadcast receiver to get notifications and when app is in foreground, emits an event for ReactNative with the data.
When the app is in quit or background state, puts the notification into a static hashmap and invokes a headless js service.

When the app is brought to foreground from quit or background state by tapping on a notification in tray, ReactNative module gets the message id from the 
intent and then checks for the message in the hashmap. If found emits an event when the app is in background, or resolves a promise with the message when 
the app is in quit state.

If a user opens the app and close it while notifications are in tray, resources are released including the hashmap and all notifications are lost. Next time 
when the user opens the app by tapping a notification, app does not receive the message.

The forked messaging library have removed the hashmap and on notification tap, message is acquired via intent extras and passed to the app.

## Steps

- clone react-native-firebase from https://github.com/invertase/react-native-firebase
- check for tags with `git tag -list '*messaging@8*'`
- create a branch from the required tag. this branch was created with the tag @react-native-firebase/messaging@8.0.1
```git checkout -b messaging-8.0.1 @react-native-firebase/messaging@8.0.1```
- switch to react-native-firebase-messaging repository and create a branch with the above tag name. ex. 8.0.1
- copy all from react-native-firebase/packages/messaging folder
- copy .gitignore from react-native-firebase/.gitignore
- remove ```**/version.js``` from .gitignore file
- copy devDependencies from react-native-firebase root package.json
- modify android/src/main/java/io/invertase/firebase/messaging/ReactNativeFirebaseMessagingReceiver.java to remove hashmap
- modify android/src/main/java/io/invertase/firebase/messaging/ReactNativeFirebaseMessagingModule.java to remove dependencies to hashmap

```bash
yarn add https://github.com/calceytechnologies/react-native-firebase-messaging#6.7.1
```

