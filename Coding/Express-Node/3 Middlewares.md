
in Routes File exampleRoutes.js

```js
const express = require('express');
const router = express.Router();
const verifyUser = require('../middlewares/verifyUser'); // Import the middleware

// Routes without middleware
router.get('/', dropController.getAll);
// Routes with middleware
router.post('/', verifyUser, dropController.create); // Verify token before accessing 

module.exports = router;
```

