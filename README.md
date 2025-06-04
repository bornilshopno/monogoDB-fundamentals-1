## 📘 MongoDB Learning Documentation

Welcome to my MongoDB learning repository! This documentation is a collection of notes, code snippets, and resources that I’ve gathered while learning MongoDB.


## 🧠 Introduction

MongoDB is a NoSQL database that stores data in flexible, JSON-like documents. It's designed for scalability and performance.


## 💻 Basic Commands

mongosh             # Start MongoDB shell

show dbs            # List databases

use testDB          # Switch to (or create) a database

show collections    # List collections in the current DB


## ✍️ BASIC CRUD Operations
```js
db.users.insertOne({ name: "Manush", age: 25 });
db.users.insertMany({ name: "Manush", age: 25 },{ name: "Human", age: 30 });
db.users.find().sort({ age:1 }).limit(10); 
//.sort(field: 1(ASC)/-1(DESC)) //.limit(number)
db.users.findOne({ name: "Manush" });
db.users.updateOne({ name: "Manush" }, { $set: { age: 26 } });
db.users.deleteOne({ name: "Manush" });

```

--------------------------------------------------

# 📚 Query: find()

below are the basic queries we use for find operation

## Field Filtering 

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

### Implicitely AND/OR

Structure==>>

**{field:condition, field:condition, field: {condition1,condition2}}**
```js
//when searching for entry with age 21-39
db.collectionName.find({ age : { $gt : 20, $lt : 40}}); 
//when searching for entry with age 21-39 AND gender:Female
db.collectionName.find({ age : { $gt : 20, $lt : 40} , gender:"Female"});
//when searching for entry with age 20 or 22 or 24(implicite OR)
db.collectionName.find({ age : { $in : [20, 22, 24]}});
```

### Explicitely AND/OR

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

## Find on Arrays

```js
//will search for specific array with elements on this order
db.collectionName.find( {interests : [ "Gardening", "Gaming", "Cooking" ] } );
//will search any array with containing the elements among all others
db.collectionName.find( {interests : {$all:[ "Gardening", "Gaming", "Cooking" ] } } );
//will search for the arrays with only of length 4
db.collectionName.find( {interests : { $size : 4} } );
//will search this key-value in array of objects
db.collectionName.find({skills:{$elemMatch: {name: "PYTHON",level : "Expert",}}}) 
```

--------------------------------------------------
--------------------------------------------------

# 📚 Query: Update Operations

Basic Structure

## updateOne(filter, updatedDOC,upsert)

## $set, $addToSet, $each, $push, $pop, $unset, $pull, $pullALL, $inc
```js



//replace the field totally
db.collectionName.updateOne({_id : ObjectId("6406ad63fc13ae5a40000069")}, 
{$set: {interests :  ["Gaming","Cooking","Reading","Dancing","Swimming"]}}) 

//adds "Reading" while keeping the rest elements if this is not present there
db.collectionName.updateOne({_id : ObjectId("6406ad63fc13ae5a40000069")}, 
{$addToSet:  {interests :  "Reading"}}) 

//adds multiple element of interest array if this is not present there
 db.collectionName.updateOne({_id : ObjectId("6406ad63fc13ae5a40000069")}, 
{$addToSet:  {interests : {$each:["Watching", "Swimming"]}}}) 

//adds even if it is exisiting already
db.collectionName.updateOne({_id : ObjectId("6406ad63fc13ae5a40000069")}, 
{$push:  {interests :  "Dancing"}}) 

//delete the last element of an array
db.collectionName.find({_id : ObjectId("6406ad63fc13ae5a40000069")},
{$pop:  {interests :  +1}}) 

//delete the first element of array
db.collectionName.updateOne({_id : ObjectId("6406ad63fc13ae5a40000069")}, 
{$pop:  {interests :  -1}}) 

//delete a property(here, birthday:25-6-98)
db.collectionName.updateOne({_id : ObjectId("6406ad63fc13ae5a40000069")}, 
{$unset: {birthday: "" }}) 

//delete an element from any index
db.collectionName.updateOne({_id : ObjectId("6406ad63fc13ae5a40000069")}, 
 {$pull:  {interests :  "Dancing"}}) 
 delete an element from any index
 

 // delete multiple value
db.collectionName.updateOne({_id : ObjectId("6406ad63fc13ae5a40000069")}, 
 {$pullAll:  {interests :  ["Reading", "Reading"]}}) 

 
 // to change single/multiple value of an object 
 db.collectionName.updateOne({_id : ObjectId("6406ad63fc13ae5a40000069")},
    {$set:{
        "address.city": "Dhaka", "address.country":"Bangladesh", "address.street":"Love Road"
    } })
   
    
//to change first position of same object in an array of object 
db.collectionName.updateOne({ _id: ObjectId("6406ad63fc13ae5a4000006a"), "education.major": "Education" },
    { $set: {  "education.$.major": "ENT"}}) //here firstly "field.key": "value" need to be used as implicit AND with filtering query


//Incremental operator (updateOne without $set)
db.collectionName.updateOne({ _id: ObjectId("6406ad63fc13ae5a4000006a")},
    {$inc: {age:5} }) //age will increase by 5

```

✅ 
This repo is prepared only for note purpose 

Md Ashraf Hossain (Manna).
