# MongoDB Cheat Sheet
MongoDB Cheat Sheet with the most needed stuff..


# Logical Query operators
- https://docs.mongodb.com/manual/reference/operator/query-logical/


## MongoDB bin locations
```bash
#windows
"C:\Program Files\MongoDB\Server\4.2\bin"
```  

<br />
<br />



 _____________________________________________________
 _____________________________________________________


<br />
<br />




## Export database with all collections to .bson
```bash
mongodump --host xx.xxx.xx.xx --port 27017 --db your_db_name --username your_user_name --password your_password --out /target/folder/path
```  


## Export specific collection with ALL fields to .json
```bash
# --jsonArray will generated one json file. If not activated solo objects will be created to each document
# --pretty will pretty print the JSON to be human read able
# https://docs.mongodb.com/manual/reference/program/mongoexport
mongoexport --jsonArray --pretty -h id.mongolab.com:60599 -u username -p password -d mydb -c mycollection -o mybackup.json
```  


<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />

# Find something..


## find next alphabetic document with used = 0 and limit to 1 item
```javascript
//sync
collection.find( {"used": 0} ).limit( 1 ).toArray(function(e, docs) { /* .. */ }); 

// async
const r = await collection.find( {"used": 0} ).limit( 1 ).toArray({});
```

<br />

## find value in same document with multiple possible matches for the same field (https://docs.mongodb.com/manual/reference/operator/query/in/)
```javascript
//sync
collection.find( {title: {$in: ['some title', 'some other title']}} ).toArray(function(e, docs) { /* .. */ }); 

// async
const r = await collection.find( {title: {$in: ['some title', 'some other title']}} ).toArray({});
```

<br />

## find multiple values in same document, only if all search values can be found (https://docs.mongodb.com/manual/reference/operator/query/and/#op._S_and)
```javascript
//sync
collection.find( { $and: [{"client_id": json?.client_id}, {"client_secret": json?.client_secret}] } ).toArray(function(e, docs) { /* .. */ }); 

// async
const r = await collection.find( { $and: [{"client_id": json?.client_id}, {"client_secret": json?.client_secret}] } ).toArray({});
```

## find multiple values in same document, only if atleast one search value can be found (https://docs.mongodb.com/manual/reference/operator/query/or/#op._S_or)
```javascript
//sync
collection.find( { $or: [{"client_id": json?.client_id}, {"client_secret": json?.client_secret}] } ).toArray(function(e, docs) { /* .. */ }); 

// async
const r = await collection.find( { $or: [{"client_id": json?.client_id}, {"client_secret": json?.client_secret}] } ).toArray({});
```



<br />




## find object id
```javascript
var ObjectId = require('mongodb').ObjectId;
var id = "5f2a40a54d054559dcc566ff";
var o_id = new ObjectId(id);

// sync 
collection.find( {"itemdetails._id":o_id} ).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.find( {"itemdetails._id":o_id} ).toArray({});
```

<br />


## find specific data
Notice that it will returns an array with all results based on your search value. 
```javascript
// sync
collection.find( {"token": token} ).toArray(function(e, docs) { /* .. */ });

// async
const verify = await collection.find( {"token": token} ).toArray({});
```
<br />

## find random document with used = 0 and limit to 1 item
```javascript
// sync
collection.aggregate([ { $match: { used: 0 } }, { $sample: { size: 1 } } ]).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate([ { $match: { used: 0 } }, { $sample: { size: 1 } } ]).toArray({});
```


<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />


# Update


## Update specific field
```javascript

var query = { url: t33n.url };
var newvalues = { $set: { used: 1 } };

//sync 
collection.updateOne(query, newvalues, function(e, res) { /* .. */ });

// async
const r = await collection.updateOne(query, newvalues);
```



<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />


# Insert


## Insert single object
```javascript
//sync
collection.insertOne(json, function(e, result) { /* .. */ });

//async
const r = await collection.insertOne(json);
```



## add timestamp to insert
```javascript
// MongoDB will automatically conert new Date() to 2020-09-14T17:04:55.281+00:00
// also nice to know your object id already includes a timestamp too..
{"created_at": new Date()}
```





<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />


# Delete


## Delete specific data
```javascript
//sync
collection.deleteOne({"id": json.id}, function(e, result) { /* .. */ });

//async
const r = await collection.deleteOne( {"id": json.id} );
```




