
src/lib/util.js

```js
import mongoose from "mongoose"

const connection = {};

export const connectToDb = async () => {
  try {
    if(connection.isConnected) {
      console.log("Using existing connection");
      return;
    }
    const db = await mongoose.connect(process.env.MONGO);
    connection.isConnected = db.connections[0].readyState;
  } catch (error) {
    console.log(error);
    throw new Error(error);
  }
};

```

src/lib/util.js

```js
import { connectToDb } from "./utils";

const login = async (credentials) => {
  try { 
    connectToDb();
    // const user = await User.findOne({ username: credentials.username });
    // return user;
  } catch (err) {
    console.log(err);
    throw new Error("Failed to login!");
  }
};
```