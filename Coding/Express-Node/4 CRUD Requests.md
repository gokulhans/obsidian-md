app.js

```js
const exampleRouter = require("./routes/exampleRoutes");
app.use("/api/example", exampleRouter);
```

routes/exampleRoutes.js

```js
const express = require("express");
const router = express.Router();
const exampleController = require('../controllers/exampleController');

// POST a new example
router.post("/", exampleController.create);

// GET all examples
router.get("/", exampleController.getAll);

// GET example by ID
router.get("/:id", exampleController.getById);

// PUT update example by ID
router.put("/:id", exampleController.updateById);

// DELETE example by ID
router.delete("/:id", exampleController.deleteById);

module.exports = router;
```

controllers/exampleControllers.js

```js
const Example = require('../models/example');

const exampleController = {
    // Create a new example
    create: async (req, res) => {
        try {
            const { name } = req.body;
            const newExample = new Example({ name });
            await newExample.save();
            res.status(201).json({ msg: 'Example created', data: newExample });
        } catch (error) {
            res.status(500).json({ msg: 'Error creating example', error: error.message });
        }
    },

    // Get all examples
    getAll: async (req, res) => {
        try {
            const examples = await Example.find();
            res.json({ msg: 'OK', data: examples });
        } catch (error) {
            res.status(500).json({ msg: 'Error fetching examples', error: error.message });
        }
    },

    // Get example by ID
    getById: async (req, res) => {
        try {
            const exampleId = req.params.id;
            const example = await Example.findById(exampleId);
            if (example) {
                res.json({ msg: 'Example found', data: example });
            } else {
                res.status(404).json({ msg: 'Example not found' });
            }
        } catch (error) {
            res.status(500).json({ msg: 'Error fetching example', error: error.message });
        }
    },

    // Update example by ID
    updateById: async (req, res) => {
        try {
            const { name } = req.body;
            const updatedExample = await Example.findOneAndUpdate({ _id: req.params.id }, { name }, { new: true });
            if (updatedExample) {
                res.json({ msg: 'Example updated', data: updatedExample });
            } else {
                res.status(404).json({ msg: 'Example not found' });
            }
        } catch (error) {
            res.status(500).json({ msg: 'Error updating example', error: error.message });
        }
    },

    // Delete example by ID
    deleteById: async (req, res) => {
        try {
            const deletedExample = await Example.findOneAndDelete({ _id: req.params.id });
            if (deletedExample) {
                res.json({ msg: 'Example deleted', data: deletedExample });
            } else {
                res.status(404).json({ msg: 'Example not found' });
            }
        } catch (error) {
            res.status(500).json({ msg: 'Error deleting example', error: error.message });
        }
    }
};

module.exports = exampleController;
```

models/example.js

```js
const mongoose = require("mongoose");
const Schema = mongoose.Schema;

const exampleSchema = new Schema(
  {
    name: {
      type: String,
      required: true,
    },
  },
  { timestamps: true }
);

module.exports = mongoose.model("Example", exampleSchema);
```

Example of data saved in database

```json
{
  "_id": {
    "$oid": "65ca3e44cf5cea627fdab81a"
  },
  "name": "aa",
  "createdAt": {
    "$date": "2024-02-12T15:50:28.279Z"
  },
  "updatedAt": {
    "$date": "2024-02-12T15:50:28.279Z"
  },
  "__v": 0
}
```

