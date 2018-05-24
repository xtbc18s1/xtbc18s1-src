---
title: "Day 8: Firebase Authentication"
weight: 4
---

<date>Thursday, May 24, 2018</date>

Morning:

* [Playlist](https://www.youtube.com/watch?v=vGMMHQfp8Vk&list=PLuT2TqJuwaY_Hj168ujFhP0w5HzmaDLfG) | [Day 8, Part 1](https://www.youtube.com/watch?v=KbKqR9PP4hE&index=92&list=PLuT2TqJuwaY_Hj168ujFhP0w5HzmaDLfG)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=uX8_DUKyTx0&list=PLuT2TqJuwaY_XxGei4xUXZn9HuTU3jBRk) | [Day 8, Part 1](https://www.youtube.com/watch?v=Gru0Bj89Ar8&index=96&list=PLuT2TqJuwaY_XxGei4xUXZn9HuTU3jBRk)

## Topics

### Local Storage

### Firebase Authentication

* 'firebase/auth'
* `authWithPopup`
* signing in and out
* handling auth state changes
* database rules

## Examples

### [Local Storage and How To Use It On Websites](https://www.smashingmagazine.com/2010/10/local-storage-and-how-to-use-it/)

### Authentication

Firebase isn't just a real-time database.  It can also provide authentication services via email/password, phone, or common third-party services like Github, Facebook, and Google. For _Noteherder_, we set up authentication via Google.

#### Step 1: Enable Google authentication in Firebase

Go to your Firebase console and click on the "Authentication" tab in the "Develop" sidebar, then click on "Sign-in method".  You'll see a list of the authentication methods allowed by Firebase.  Click on "Google" and then enable the toggle switch.

#### Step 2: Add Firebase auth to your app

_Note: This step assumes you already have your Firebase database added to your app._ 

Import `firebase/auth` into your app's firebase setup.  Enable firebase auth and also create an instance of `GoogleAuthProvider`.

**base.js**

{{< code lang="js" line="4,17,18" class="line-numbers" >}}
import Rebase from 're-base'
import firebase from 'firebase/app'
import from 'firebase/database'
import 'firebase/auth'

const app = firebase.initializeApp({
  apiKey: "YOURAPIKEY",
  authDomain: "YOURAUTHDOMAIN",
  databaseURL: "YOURDATABASEURL",
  projectId: "YOURPROJECTID",
  storageBucket: "YOURSTORAGEBUCKET",
  messagingSenderId: "YOURSENDERID"
})

const db = firebase.database(app)

export const auth = app.auth()
export const googleProvider = new firebase.auth.GoogleAuthProvider()

export default Rebase.createClass(db)
{{< /code >}}

#### Step 3: Set up the SignIn Component

Import `auth` and the `googleProvider` into whatever component handles the sign-in process.  Call `signInWithPopup` on the `auth` object, passing the provider as a parameter.  This will launch a popup screen that will prompt the user to sign in using the provider you have specified.

**SignIn.js**

{{< code jsx >}}
import React from 'react'
import { auth, googleProvider } from './base'

const SignIn = () => {
  const authenticate = (provider) => {
    auth.signInWithPopup(provider)
  }

  return (
    &lt;button className="SignIn" onClick={() => authenticate(googleProvider)}&gt;
      Sign In With Google
    &lt;/button&gt;
  )
}

export default SignIn
{{< /code >}}

#### Step 4: Handling auth state changes (and page refreshes)

Once the user has authenticated via the popup, the state of our authorization has changed (we now have an authenticated user).  Other events that can cause auth state changes are signing out, timeouts, and page refreshes.  We should probably set up something to listen for these events.  In the `componentWillMount` lifecycle hook that runs when the Component is first getting loaded, we can call the `onAuthStateChanged` method provided on the global `auth` object to set up such a listener.

**App.js**

{{< code js >}}
// ...

componentWillMount() {
  auth.onAuthStateChanged(
    (user) => {
      if (user) {
        // finish signing in
        this.authHandler(user)
      } else {
        // finished signing out
        this.setState({ uid: null })
      }
    }
  )
}

// ...
{{< /code >}}

#### Step 5: Finishing sign-in

What the `authHandler` callback does is up to you, but for _Noteherder_, we had it do pretty typical things - save the user ID to state, and initialize syncing our local state for 'notes' with the data stored on Firebase.

**App.js**

{{< code js >}}
// ...

authHandler = (user) => {
  this.setState(
    { uid: user.uid },
    this.syncNotes
  )
}

// ...
{{< /code >}}

#### Step 6: Signing out

Signing out when using Firebase for authentication is also simple - just call `auth.signOut()`!  Once the promise returned by `signOut` has resolved, you can handle any additional cleanup.  In _Noteherder_, we stop syncing with Firebase and set `state.notes` back to an empty object.

**App.js**

{{< code js >}}
// ...

signOut = () => {
  auth
    .signOut()
    .then(
      () => {
        // stop syncing with Firebase
        base.removeBinding(this.ref)
        this.setState({ notes: {} })
      }
    )
}

// ...
{{< /code >}}

### Rules

For your Firebase database, you can set up rules (written in JSON) that specify the conditions under which data is allowed to be read or written.  By default, a newly generated project will require that a user be authenticated to read or write _any_ data.

{{< code js >}}
{
  "rules": {
    ".read": "auth != null",
    ".write": "auth != null"
  }
}
{{< /code >}}

If you do not have authentication set up yet, these values can be set to `true`.  This allows _anyone_ to read or write any data in the database.  This can be convenient, but probably not a good idea long-term (and you _will_ get a warning if you do that).

Additional rules can be applied per endpoint:

{{< code js >}}
{
  "rules": {
    "emails": {
      ".read": true,
      ".write": "auth != null"
    },
    "texts": {
      ".read": true,
      ".write": "auth != null"
    },
    "users": {
      "$userId": {
        ".read": "auth != null && auth.uid == $userId",
        ".write": "auth != null && auth.uid == $userId"
      }
    }
  }
}
{{< /code >}}

The above rules translate to:

* texts and emails can be read by anyone, but only written by authenticated users
* users data can be read and written only by an authenticated user whose `uid` matches the `$userId` of that item

## Projects

Noteherder: [Morning](https://github.com/xtbc18s1/noteherder) | [Afternoon](https://github.com/xtbc18s1/noteherder/tree/afternoon)

## Homework

* Add Google authentication.

### Bonus Credit

* If you're signed in, it briefly shows the `SignIn` component before showing `Main`. Fix that! Try storing `uid` in `localStorage`.

### Super Mega Bonus Credit

* Scope notes by user. Let each user have their own array of notes. (Try changing the _endpoint_ argument to `base.syncState()`.)


