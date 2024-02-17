```
generate routes according to this model

SYNTAX

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

MODEL

<<< PASTE YOUR MODEL >>>


```