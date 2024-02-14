Create a folder with project name.

Open folder in VS Code.

Create folder Frontend.
Create folder Backend.
#### Create FEATURES.md.

```
## App Features

### User
- [ ] **Authentication**

Check the boxes once each feature is implemented and tested successfully. Happy coding!
```
#### Create LICENSE.

```
MIT License

Copyright (c) 2023 Fundx

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

#### Create README.md.

```
# App Name

App Description

Visit [App Name](https://www.app-link.com/) to kickstart your journey.

## Why App Name ?

More Description.

## Get Started

More Details to get going.
```

#### Open Backend Folder

```
npm init -y
```

```
npm i express bcrypt cors jsonwebtoken dotenv mongoose nodemon
```

#### Create app.js 

```js
const express = require("express");
const app = express();
const cors = require("cors");
const db = require("./db");
require("dotenv").config();

app.use(express.json());

app.use(cors());

const userRouter = require("./routes/userRoutes");

app.use("/api/user", userRouter);

app.get("/", (req, res) => {
  res.json({ message: "Hello World!" });
});

app.listen(process.env.PORT || 5000, () =>
  console.log("Server is running on port 5000")
);
```

#### Create folders

```
routes
controllers
models
config
middlewares
```

#### Create routes/userRoutes.js

```js
const express = require("express");
const router = express.Router();
const userController = require('../controllers/userController');

// GET all users
router.get("/", userController.getAll);

// GET user by ID
router.get("/:id", userController.getById);

// POST a new user
router.post("/", userController.create);

// UPDATE user by ID
router.put("/:id", userController.updateById);

// DELETE user by ID
router.delete("/:id", userController.deleteById);

module.exports = router;
```

#### Create controllers/userControllers.js

```js
const User = require('../models/user');

const userController = {
    create: async (req, res) => {
        try {
            const { name, email, password } = req.body;
            const newUser = new User({ name, email, password });
            await newUser.save();
            res.json({ msg: 'User created', data: newUser });
        } catch (error) {
            res.status(500).json({ msg: 'Error creating user', error: error.message });
        }
    },
    getAll: async (req, res) => {
        try {
            const users = await User.find();
            res.json({ msg: 'OK', data: users });
        } catch (error) {
            res.status(500).json({ msg: 'Error fetching users', error: error.message });
        }
    },
    getById: async (req, res) => {
        try {
            const userId = req.params.id;
            const user = await User.findById(userId);
            if (user) {
                res.json({ msg: 'User found', data: user });
            } else {
                res.status(404).json({ msg: 'User not found' });
            }
        } catch (error) {
            res.status(500).json({ msg: 'Error fetching user', error: error.message });
        }
    },
    updateById: async (req, res) => {
        try {
            const { name, email, password } = req.body;
            const updatedUser = await User.findOneAndUpdate({ _id: req.params.id }, { name, email, password }, { new: true });
            if (updatedUser) {
                res.json({ msg: 'User updated', data: updatedUser });
            } else {
                res.status(404).json({ msg: 'User not found' });
            }
        } catch (error) {
            res.status(500).json({ msg: 'Error updating user', error: error.message });
        }
    },
    deleteById: async (req, res) => {
        try {
            const deletedUser = await User.findOneAndDelete({ _id: req.params.id });
            if (deletedUser) {
                res.json({ msg: 'User deleted', data: deletedUser });
            } else {
                res.status(404).json({ msg: 'User not found' });
            }
        } catch (error) {
            res.status(500).json({ msg: 'Error deleting user', error: error.message });
        }
    }
};

module.exports = userController;
```

#### Create models/user.js

```js
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const userSchema = new Schema({
    name: {
        type: String,
        required: true
    },
    email: {
        type: String,
        required: true,
        unique: true
    },
    password: {
        type: String,
    },
    photoURL: {
        type: String,
    },
    googleId: {
        type: String,
    },
    isBlocked: {
        type: Boolean,
        default: false  // Default value is set to false, indicating the user is not blocked initially
    }
},
    { timestamps: true }
);

module.exports = mongoose.model('User', userSchema);
```

#### Create middlewares/verifyToken.js

```js
const jwt = require('jsonwebtoken');
const secretKey = process.env.JWT_SECRET_KEY; // Replace with a secure secret key

const verifyToken = (req, res, next) => {
    const token = req.header('Authorization').replace('Bearer ', '');
    // if (req.isAuthenticated()) {
    //     return next();
    // }
    try {
        const decoded = jwt.verify(token, secretKey);
        // If verification is successful, attach the user data to the request object
        req.user = decoded;
        next(); // Proceed to the protected route
    } catch (error) {
        res.status(401).json({ error: 'Authentication failed' });
    }
};

module.exports = verifyToken;
```

#### Create config/db.config.js

```js
require('dotenv').config()

module.exports = {
    uri: process.env.MONGODB_URI
};
```

#### Create .gitignore

```gitignore
node_modules/
.env
```

#### Create db.js

```js
const mongoose = require("mongoose");
const mongoconfig = require('./config/db.config');

mongoose.set("strictQuery", false);

const mongouri = mongoconfig.uri;

run().catch((err) => console.log(err));

async function run() {
    await mongoose.connect(mongouri);
    console.log('Connected to the database');
}
```

#### Create vercel.json

```json
{
    "version": 2,
    "builds": [
        {
            "src": "app.js",
            "use": "@vercel/node",
            "config": {
                "includeFiles": [
                    "dist/**"
                ]
            }
        }
    ],
    "routes": [
        {
            "src": "/(.*)",
            "dest": "app.js"
        }
    ]
}
```

#### Create .env

```env
MONGODB_URI=mongodb+srv://test:testdb.joiejrf.mongodb.net/?retryWrites=true&w=majority
JWT_SECRET_KEY=my-jwt-token
PORT=5000
```

#### Edit Package.json

```json
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node app.js",
    "dev": "nodemon app.js"
  },
```
