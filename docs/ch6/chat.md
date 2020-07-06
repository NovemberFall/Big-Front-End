# chat-firebase

# Vue
### how to run VUE
- `npm run dev`

### if you want to change port:
- `npm run serve -- --port 3000`


### vue-cli
- `npm install -g @vue/cli`
---

### webpack
![](img/2019-11-06-10-40-44.png)
---
- `npm install -g @vue/cli-init`
![](img/2019-11-06-10-41-26.png)
---
- `vue init webpack music-chat`
![](img/2019-11-06-10-44-39.png)
- choose use NPM


### how to run vue.js
- cd to the project folder
- `npm run dev`
![](img/2019-11-06-11-22-09.png)
---





---
firebase + online chat

- `console.firebase.google.com`
- `music-chat`
![](img/2019-11-06-09-30-37.png)
---
- click database
![](img/2019-11-06-09-34-59.png)
---
![](img/2019-11-06-09-39-48.png)
---
![](img/2019-11-06-10-03-22.png)
---
- go to Project Overview
![](img/2019-11-06-10-04-27.png)
---
![](img/2019-11-06-10-08-50.png)
- choose `web`
- copy and paste
```js
// Your web app's Firebase configuration
var firebaseConfig = {
    apiKey: "AIzaSyD-VyAXCSh-4cyp4FWLflbNF6R1-BMTkhE",
    authDomain: "music-online-chat.firebaseapp.com",
    databaseURL: "https://music-online-chat.firebaseio.com",
    projectId: "music-online-chat",
    storageBucket: "music-online-chat.appspot.com",
    messagingSenderId: "34846148953",
    appId: "1:34846148953:web:633d14870d629b85036448"
};
// Initialize Firebase
firebase.initializeApp(firebaseConfig);
```
![](img/2019-11-06-10-10-56.png)
---


### Firestore Setup
- create a new foler `firebase`
- create a new init.js
![](img/2019-11-06-10-50-16.png)
---
- copy this codes into init.js
![](img/2019-11-06-10-51-41.png)
---
- then run `npm install firebase@4.13`
---
