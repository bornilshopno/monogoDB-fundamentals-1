📘 MongoDB Learning Documentation

Welcome to my MongoDB learning repository! This documentation is a collection of notes, code snippets, and resources that I’ve gathered while learning MongoDB.


🧠 Introduction

MongoDB is a NoSQL database that stores data in flexible, JSON-like documents. It's designed for scalability and performance.


💻 Basic Commands

mongosh             # Start MongoDB shell
show dbs            # List databases
use testDB          # Switch to (or create) a database
show collections    # List collections in the current DB


✍️ BASIC CRUD Operations
```js
db.users.insertOne({ name: "Manush", age: 25 });
db.users.insertMany({ name: "Manush", age: 25 },{ name: "Human", age: 30 });
db.users.find();
db.users.findOne({ name: "Manush" });
db.users.updateOne({ name: "Manush" }, { $set: { age: 26 } });
db.users.deleteOne({ name: "Manush" });

```

--------------------------------------------------

📚 Query Formats

below are the basic some key notes for querying

##Field Filtering 

==>> to only find specific(name,email) fields on result

```js
db.collectionName.find({},{name:1, email:1});
db.collectionName.find().project{name:1, email:1}
```

##Comparison Operators

==>>**{always need to be used inside currly braces}**

==>> $eq, $neq, $gt, $gte, $lt, $lte

==>> $in, $nin <more or less similar to OR>


```js
//same for $eq, $neq, $gte, $lt, $lte
db.collectionName.find({ age : { $gt : 20}});
//same for $nin <not in>
db.collectionName.find({ age : { $in : [20, 22, 24]}});
```


## AND,OR operators 

We can handle AND & OR both implicitely and explicitely in MONGODB.

### Implicitely AND

Structure==>>

**{field:condition, field:condition, field: {condition1,condition2}}**
```js
//when searching for entry with age 21-39
db.collectionName.find({ age : { $gt : 20, $lt : 40}}); 
//when searching for entry with age 21-39 AND gender:Female
db.collectionName.find({ age : { $gt : 20, $lt : 40} , gender:"Female"});
```

### Explicitely AND

Structure==>>

**{$and: [ {field:condition}, {field:condition}, {field:condition}]}**
**{$or: [ {field:condition}, {field:condition}, {field:condition}]}**

```js
//when searching for entries with age 21-39
db.collectionName.find( { $and : [ {age: {$gt :20}}, {age :{$lt :40}} ] } );
//when searching for entries with age 21-39 AND gender:Female
db.collectionName.find( { $and : [ {age: {$gt :20}}, {age :{$lt :40}}, { gender :"Female"} ] } ); 

//when searching for entries with age<20 and age>40
db.collectionName.find( { $or : [ {age: {$gt :40}}, {age :{$lt :20}} ] } );
```



✅ About
This project is maintained by Md Ashraf Hossain (Manna).
Feel free to fork, clone, or contribute!