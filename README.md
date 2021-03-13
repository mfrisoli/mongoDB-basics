# mongoDB basics guide

Hello, All! 

This repository part of a project that I have started to keep notes on relevant courses and new technologies. The idea of this is to practice the skills while doing the repo and to help others in their learning journey by providing summaries or quick consultation guides.

Disclaimer: By no means this replaces official documentation.

## Table of Contents

- **[What is MongoDB Database](#What-is-MongoDB-Database)**<br>
- **[JSON and BSON (from mongoDB)](#JSON-and-BSON-(from-mongoDB))**<br>
- **[Terms](#Terms)**<br>
- **[How to Install MongoDB](#How-to-Install-MongoDB)**<br>
- **[How to Connect to a mongoDB cluster](#How-to-Connect-to-a-mongoDB-cluster)**<br>
- **[Navigating the shell](#Navigating-the-shell)**<br>
- **[Creating](#Creating)**<br>


- **[References](#References)**<br>

## What is MongoDB Database

MongoDB is a NoSQL document database. it stores data in an organized way but not in rows and columns. Data is stored as documents and these documents are then stored in a collection of documents.

A *Database* is a collection of information that is organized and structured in a way to store and access data.

a *Document* is a way to organize and store data as a set of field-value pairs. the field is a unique identifier in the document. the structure looks similar to JSON.

```JSON
 {"<field>":<key>}
```

A *Collection* contains multiple documents and a Database contains multiple collections.

##  [JSON and BSON (from mongoDB)](https://www.mongodb.com/json-and-bson):

"JavaScript Object Notation (JSON) are simple associative containers, wherein a string key is mapped to a value (which can be a number, string, function, or even another object). JSON is represented in text.

BSON stands for “Binary JSON” BSON’s binary structure encodes type and length information, which allows it to be parsed much more quickly.


Languages that support any kind of complex mathematics typically have different sized integers (ints vs longs) or various levels of decimal precision (float, double, decimal128, etc.).

Not only is it helpful to be able to represent those distinctions in data stored in MongoDB, it also allows for comparisons and calculations to happen directly on data in ways that simplify consuming application code."

<br>

## Terms
- _id Field:

- Namespace is a notation of a database and collection name

```
database.collection
```


## How to Install MongoDB


## How to Connect to a mongoDB cluster

You should be able to connect to a mongoDB cluster using either of the following commands in the mongo shell:

```
$ mongo "mongodb+srv://<username>:<password>@<cluster>.mongodb.net/admin" 
``` 
or
```
$ mongo "mongodb+srv://<cluster>.mongodb.net/<database>" --username <username> --password <password>
```
## Navigating in the shell
To navigate the mongoDB shell you can use the following commands:

### Show databases

```
show dbs
```

### To use a particular database
```
use <database>
```

### Show Collections
```
show collections
```

## Simple Queries

**find()** method returns a cursor with a document match
```JSON
$ db.<collection>.find( { <field>:<key> } )
```

Example:
```JSON
$ db.mycollection.find( { "name":"John" } )
```

**count()** is a method that will return the number of documents that match a particular condition, it can follow after the find() method.

Example:
```JSON
$ db.mycollection.find( { "name":"John" } ).count()
```


A very helpful method is **pretty()**. this will format the cursor into a redable output easier to read 

Example:
```JSON
$ db.mycollection.find( { "name":"John" } ).pretty()
```

tip: you can use `db.<collection>.findOne().pretty()` to have a look at all the fields inside a sample document, note that his will select a document randomly.

## Query Selectors

These are examples and brief summary on a select number of operators, the [mongoDB documentation](https://docs.mongodb.com/manual/reference/operator/query/) covers this perfectly! so for all the other operators you can check the documentation.

### Comparison Example:

**$gte**: greater than or equal

```JSON
db.<collection>.find( {
    <field> : { $gte : <numeric> }
} ).pretty()

```


### Logical Example

**$or** & **$and** example:
```JSON
db.<collection>.find({ "$and": [
     { "$or" :[{ "<field>": "<match>" }, { "<field>": "<match>" }]},
     { "$or" :[ { "<field>": "<match>" },{ "<field>": "<match>" }]}
    ]}).pretty()
```

**$and** example:
```JSON
db.<collection>.find({
    $and:[
        { '<field>':"<match>" },
        { 'field':'<match>' }
    ]
}).pretty()

```

### Evaluation:

**$exp**, this operator allows you to compare the value of two different fields. Assuming the following scenario. A collection where documents have fields of "name" and "parent name", we can return all documents where the name and parent name are equal using the below example. make sure to include "$"

```JSON
db.<collection>.find({"$expr":
    { 
        $eq: [ "$<field_1>", "$<field_2>"]
    }}).count()
```

## Creating

### Database
For creating a database you can simply use "`use newDB`" in the mongo shell, if the DB does not exist, a new DB will be created.

<br>

### Collection & Document
The simplest way to create a collection is using the [insertOne()](https://docs.mongodb.com/manual/reference/method/db.collection.insertOne/#db.collection.insertOne) method. There is also an explicit method for creating a collection, check out this link [Explicit Creation](https://docs.mongodb.com/manual/reference/method/db.createCollection/#db.createCollection).

```JSON
db.<newCollection>.insertOne( { <field>: <key> } )
```

Example:
```JSON
db.newcollection.insertOne( { 
    "name": "John",
    "lastname": "Doe",
    "birth_year": 2009
 } )
```

This command will create a new collection called "`newcollection`" and will also insert a document. Unless explicitly expressed, MongoDB will automatically create the _id field and generate a unique key for the document.

In this example, if the collection already existed, it will only insert a new document.


## More information

Want to know more? I highly recommend you visit the official [mongoDB University](https://university.mongodb.com/) website and check out their courses.

## References:

- [GitHub Flavored Markdown](https://docs.github.com/en/github/writing-on-github/basic-writing-and-formatting-syntax#ignoring-markdown-formatting)
- [Adam P: Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
- [mongoDB University](https://university.mongodb.com/)