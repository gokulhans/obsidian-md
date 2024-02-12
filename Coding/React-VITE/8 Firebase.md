
Create firebase.js

```js
import { initializeApp } from 'firebase/app'
import { getAnalytics } from 'firebase/analytics'
import { getAuth } from 'firebase/auth'
import { GoogleAuthProvider } from 'firebase/auth'
import { getFirestore } from 'firebase/firestore'

const firebaseConfig = {
    apiKey: import.meta.env.VITE_FIREBASE_API_KEY,
    authDomain: import.meta.env.VITE_FIREBASE_AUTH_DOMAIN,
    projectId: import.meta.env.VITE_FIREBASE_PROJECT_ID,
    storageBucket: import.meta.env.VITE_FIREBASE_STORAGE_BUCKET,
    messagingSenderId: import.meta.env.VITE_FIREBASE_MESSAGING_SENDER_ID,
    appId: import.meta.env.VITE_FIREBASE_APP_ID,
    measurementId: import.meta.env.VITE_FIREBASE_MEASUREMENT_ID,
};


const app = initializeApp(firebaseConfig)
const analytics = getAnalytics(app)
export const auth = getAuth(app)
export const db = getFirestore(app)
export const provider = new GoogleAuthProvider()
```

Add this on .env file.

```
VITE_FIREBASE_API_KEY=AIzaSxxxxxxxxvZmtUD4E
VITE_FIREBASE_AUTH_DOMAIN=codexxxxxxxxeapp.com
VITE_FIREBASE_PROJECT_ID=codexxxxxxxx35d2
VITE_FIREBASE_STORAGE_BUCKET=codedrxxxxxxxxot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=12480xxxxxxxx097
VITE_FIREBASE_APP_ID=1:12480xxxxxxxx93edcd5e23cd4f8
VITE_FIREBASE_MEASUREMENT_ID=G-xxxxxxxxX2RC
```