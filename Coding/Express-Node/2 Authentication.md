
```
Set Routes on app.js file.
```

Create routes/authRoutes.js

```js
const express = require("express");
const router = express.Router();

const authController = require('../controllers/authControllers');

// User Signup and Signin
router.post("/signup", authController.signUp);
router.post("/signin", authController.signIn);
router.post("/google/signin", authController.googleSignIn);

// Admin Signup and Signin
router.post("/admin/signup", authController.signUpAdmin);
router.post("/admin/signin", authController.signInAdmin);

module.exports = router;
```

Create controllers/authControllers.js

```js
const User = require('../models/user');
const Admin = require('../models/admin');
const bcrypt = require('bcrypt');
const jwt = require('jsonwebtoken');

const authController = {
    googleSignIn: async (req, res) => {
        const { name, email, photoURL, _id } = req.body;

        const newUser = new User({
            name,
            email,
            password: "",
            photoURL,
            googleId: _id
        });
        try {
            const user = await User.findOne({ email });
            // If the user doesn't exist
            if (!user) {
                await newUser.save();
                const token = jwt.sign({ userId: newUser._id, email: newUser.email }, process.env.JWT_SECRET_KEY, {
                    // expiresIn: '1h', // Token expiration time (e.g., 1 hour)
                });
                res.status(201).json({ message: 'User created successfully', name, userId: newUser._id, token, email, photoURL });
            } else {

                // Generate a JSON Web Token (JWT)
                const token = jwt.sign({ userId: user._id, email: user.email }, process.env.JWT_SECRET_KEY, {
                    // expiresIn: '1h', // Token expiration time (e.g., 1 hour)
                });
                // Send the token and user details in the response
                res.status(200).json({ message: 'Sign in successful', userId: user._id, name: user.name, token, email, photoURL });
            }

        } catch (error) {
            if (error.code === 11000 && error.keyPattern && error.keyPattern.email) {
                return res.status(400).json({ error: 'Email address is already in use' });
            }
            console.error(error);
            res.status(500).json({ error: 'Internal Server Error' });
        }
    },
    signUp: async (req, res) => {
        const { name, email, password, confirmPassword, acceptTerms } = req.body;

        // Hash the password
        const saltRounds = 10;
        const hashedPassword = await bcrypt.hash(password, saltRounds);

        // Create a new user instance
        const newUser = new User({
            name,
            email,
            password: hashedPassword,
            acceptTerms,
        });

        try {
            // Save the user to the database
            await newUser.save();

            // Generate a JSON Web Token (JWT)
            const token = jwt.sign({ userId: newUser._id, email: newUser.email }, process.env.JWT_SECRET_KEY, {
                // expiresIn: '1h', // Token expiration time (e.g., 1 hour)
            });

            // Send the token and user details in the response
            res.status(201).json({ message: 'User created successfully', name, userId: newUser._id, token, email });
        } catch (error) {
            // Handle specific Mongoose duplicate email error
            if (error.code === 11000 && error.keyPattern && error.keyPattern.email) {
                return res.status(400).json({ error: 'Email address is already in use' });
            }
            // Handle other errors
            console.error(error);
            res.status(500).json({ error: 'Internal Server Error' });
        }
    },
    signIn: async (req, res) => {
        const { email, password } = req.body;

        try {
            // Check if the user with the provided email exists in the database
            const user = await User.findOne({ email });

            // If the user doesn't exist, return an error
            if (!user) {
                return res.status(401).json({ error: 'Invalid email or password' });
            }

            // Verify the provided password with the stored hashed password
            const isPasswordValid = await bcrypt.compare(password, user.password);

            // If the password is invalid, return an error
            if (!isPasswordValid) {
                return res.status(401).json({ error: 'Invalid email or password' });
            }

            // Generate a JSON Web Token (JWT)
            const token = jwt.sign({ userId: user._id, email: user.email }, process.env.JWT_SECRET_KEY, {
                // expiresIn: '1h', // Token expiration time (e.g., 1 hour)
            });

            // Send the token and user details in the response
            res.status(200).json({ message: 'Sign in successful', userId: user._id, name: user.name, token, email });
        } catch (error) {
            console.error(error);
            res.status(500).json({ error: 'Internal Server Error' });
        }
    },
    // Admin signUp
    signUpAdmin: async (req, res) => {
        const { name, email, password } = req.body;

        // Check if the user's email matches the admin email you want to allow
        const allowedAdminEmails = ['admin1@example.com',];

        // Check if the provided email is in the list of allowed admin emails
        if (allowedAdminEmails.includes(email)) {

            // Hash the password
            const saltRounds = 10;
            const hashedPassword = await bcrypt.hash(password, saltRounds);

            // Create a new admin instance
            const newAdmin = new Admin({ name, email, password: hashedPassword });
            try {
                // Save the admin to the database
                await newAdmin.save();

                // Generate a JSON Web Token (JWT)
                const token = jwt.sign({ adminId: newAdmin._id, email: newAdmin.email }, process.env.JWT_SECRET_KEY, {
                    // expiresIn: '1h', // Token expiration time (e.g., 1 hour)
                });

                // Send the token and admin details in the response
                res.status(201).json({ message: 'Admin created successfully', name, adminId: newAdmin._id, token, email });
            } catch (error) {
                // Handle specific Mongoose duplicate email error
                if (error.code === 11000 && error.keyPattern && error.keyPattern.email) {
                    return res.status(400).json({ error: 'Email address is already in use' });
                }
                // Handle other errors
                console.error(error);
                res.status(500).json({ error: 'Internal Server Error' });
            }
        } else {
            return res.status(403).json({ error: 'Forbidden: You are not authorized to register as an admin' });
        }
    },
    // Admin signin
    signInAdmin: async (req, res) => {
        const { email, password } = req.body;

        try {
            // Check if the admin with the provided email exists in the database
            const admin = await Admin.findOne({ email });

            // If the admin doesn't exist, return an error
            if (!admin) {
                return res.status(401).json({ error: 'Invalid email or password' });
            }

            // Verify the provided password with the stored hashed password
            const isPasswordValid = await bcrypt.compare(password, admin.password);

            // If the password is invalid, return an error
            if (!isPasswordValid) {
                return res.status(401).json({ error: 'Invalid email or password' });
            }

            // Generate a JSON Web Token (JWT)
            const token = jwt.sign({ adminId: admin._id, email: admin.email }, process.env.JWT_SECRET_KEY, {
                // expiresIn: '1h', // Token expiration time (e.g., 1 hour)
            });

            // Send the token and admin details in the response
            res.status(200).json({ message: 'Sign in successful', adminId: admin._id, name: admin.name, token, email });
        } catch (error) {
            console.error(error);
            res.status(500).json({ error: 'Internal Server Error' });
        }
    },

};

module.exports = authController;
```

Create User Model models/user.js

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

Create Admin Model models/admin.js

```js
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const adminSchema = new Schema({
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
        required: true
    },
    isBlocked: {
        type: Boolean,
        default: false  // Default value is set to false, indicating the user is not blocked initially
    }
},
    { timestamps: true }
);

module.exports = mongoose.model('Admin', adminSchema);
```

Create middlewares/VerifyUser.js

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

module.exports = verifyUser;
```

Create middlewares/VerifyAdmin.js

```js
const jwt = require('jsonwebtoken');
const Admin = require('../models/admin');

const verifyAdmin = async (req, res, next) => {
    const token = req.header('Authorization').replace('Bearer ', '');

    try {
        // Verify the token
        const decoded = jwt.verify(token, process.env.JWT_SECRET_KEY);
        const admin = await Admin.findOne({ _id: decoded.adminId, email: decoded.email });

        if (!admin) {
            throw new Error();
        }

        // Attach the admin object to the request for further processing
        req.admin = admin;
        next();
    } catch (error) {
        res.status(401).json({ error: 'Not authorized to access this resource' });
    }
};

module.exports = verifyAdmin;
```