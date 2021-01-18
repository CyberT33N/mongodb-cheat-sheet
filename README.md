# MongoDB Cheat Sheet
MongoDB Cheat Sheet with the most needed stuff..


# Guides
- MongoDB Course (https://university.mongodb.com/courses/M220JS/about)
- The MongoDB Aggregation Framework (https://university.mongodb.com/courses/M121/about)











<br><br>
____________________________________________________
____________________________________________________
<br><br>

# WEB GUI
- https://github.com/mongo-express/mongo-express











<br><br>
____________________________________________________
____________________________________________________
<br><br>


# MongoDB Compass
- Desktop GUI for showing local or remote Database.

## Install
- https://www.mongodb.com/try/download/compass

#### Ubuntu
```bash
sudo dpkg -i 'mongodb-compass_1.23.0_amd64.deb'
```


<br><br>

## Uninstall

#### Ubuntu
```bash
sudo dpkg --remove mongodb-compass
```

<br><br>

## Features
- Export Aggregations to Code
- Manage Connections
- Export Database to .json and .csv
- View Databases


































<br><br>
____________________________________________________
____________________________________________________
<br><br>


# Server

<br><br>

## Windows

<br><br>

#### Set Environment Variable
- In some cases you may not able to use **mongo** in your terminal. To fix this **Right Click Computer > Settings > Advanced Settings > Environment Variables > System Variables > Edit > New
```bash
C:\Program Files\MongoDB\Server\4.4\bin;
```













## Community Server
- https://www.mongodb.com/try/download/community

<br><br>
#### MAC
Install Terminal Command:
```bash
brew install mongodb
```
Start Command:
```bash
brew services start mongodb
```
Stop Command:
```bash
brew services stop mongodb
```

<br><br>

#### Fedora:
Install Command:
```bash
sudo dnf install downloadedpackage.rpm
```
Start Command:
```bash
sudo service mongod start
```
Stop Command:
```bash
sudo service mongod stop
```
Enable in general:
```bash
sudo systemctl enable mongod
```

<br><br>

#### CentOS:
Install Command:
```bash
sudo rpm -i downloadedpackage.rpm
```
Start Command:
```bash
sudo service mongod start
```
Stop Command:
```bash
sudo service mongod stop
```
Enable in general:
```bash
sudo systemctl enable mongod
```

<br><br>

#### Ubuntu:
Start Command:
```bash
sudo service mongod start
```
Stop Command:
```bash
sudo service mongod stop
```
Enable in general:
```bash
sudo systemctl enable mongod
```

<br><br>

#### Windows:
- MongoDB Server should get an autostart entry by default after installation.
Start Command:
```bash
net start MongoDB
```
Stop Command:
```bash
net stop MongoDB
```










<br><br><br><br>



## Enterprise Server
- https://www.mongodb.com/try/download/enterprise


#### Guides
- https://docs.mongodb.com/manual/administration/install-enterprise/




























<br><br>
____________________________________________________
____________________________________________________
<br><br>


# Docker

## docker-compose
```yml
version: '3.7'
services:
  mongodb_container:
    image: mongo:latest
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: testpw
    ports:
      - 27017:27017
    volumes:
      - mongodb_data_container:/data/db

volumes:
  mongodb_data_container:
```





























<br><br>

____________________________________________________
____________________________________________________

<br><br>

# Connection String (https://docs.mongodb.com/manual/reference/connection-string/index.html)

<br><br>

## srv (service record)
- connect to database
- username and password data is stored in database
- host will only host the srv. srv will define its own DNS with list of hostnames where we resolve.
- database is the cluster where will connect to
- We can change the server inside of the srv without doing any changes at the client side app.
```bash
mongodb+srv://username:password@host/database

# example
mongodb+srv://username:password@any-example.mongodb.net/admin

# specify options
mongodb+srv://username:password@any-example.mongodb.net/admin?retryWrites=true
```

<br><br>

## Standard URI
```bash
# standalone
mongodb://mongodb0.example.com:27017

# For a standalone that enforces access control (https://docs.mongodb.com/manual/tutorial/enable-authentication/):
mongodb://myDBReader:D1fficultP%40ssw0rd@mongodb0.example.com:27017/?authSource=admin
```



<br><br>

## localhost URI
- mongodb://localhost:27017














































<br><br>

____________________________________________________
____________________________________________________

<br><br>

# CLI


## MongoDB bin locations
```bash
#windows
"C:\Program Files\MongoDB\Server\4.2\bin"
```

<br><br>


## Export database with all collections to .bson
```bash
mongodump --host xx.xxx.xx.xx --port 27017 --db your_db_name --username your_user_name --password your_password --out /target/folder/path
```

<br><br>


## Export specific collection with ALL fields to .json
```bash
# --jsonArray will generated one json file. If not activated solo objects will be created to each document
# --pretty will pretty print the JSON to be human read able
# https://docs.mongodb.com/manual/reference/program/mongoexport
mongoexport --jsonArray --pretty -h id.mongolab.com:60599 -u username -p password -d mydb -c mycollection -o mybackup.json
```

<br><br>


## Mongo Shell

<br><br>

#### run and load .js files via mongo shell
```javascript
/* // validateLab1.js
var validateLab1 = pipeline => {
  let aggregations = db.getSiblingDB("aggregations")
  if (!pipeline) {
    print("var pipeline isn't properly set up!")
  } else {
    try {
      var result = aggregations.movies.aggregate(pipeline).toArray().length
      let sentinel = result
      let data = 0
      while (result != 1) {
        data++
        result = result % 2 === 0 ? result / 2 : result * 3 + 1
      }
      if (sentinel === 23) {
        print("Answer is", data)
      } else {
        print("You aren't returning the correct number of documents")
      }
    } catch (e) {
      print(e.message)
    }
  }
}
*/

# enter mongo shell
mongo

# define pipeline
var pipeline = [{$match: { 'imdb.rating': {'$gte': 7}, 'genres': {'$ne': ['Crime', 'Horror']}, 'languages': {'$eq': ['English', 'Japanese']} }}]

# load the js file
load('validateLab1.js')

# run the js file
validateLab1(pipeline)
```
































<br><br>

____________________________________________________
____________________________________________________

<br><br>

# Connection (http://mongodb.github.io/node-mongodb-native/2.1/reference/connecting/connection-settings/)
- Always handle the **serverSelectionTimeout** in your error catch to check where any server gets down or when any problems happen
```javascript
let myDB;
var MongoClient = require('mongodb').MongoClient;



const MongoDB_DB_URL =
const options = {
  authSource: "admin", // This is the name of the cluster database that has the collection with the user credentials. For default it will be admin (https://docs.mongodb.com/manual/reference/connection-string/#urioption.authSource)
  useNewUrlParser: true,
  useUnifiedTopology: true,
  connectTimeoutMS: 200,
  retryWrites: true,
  poolSize: 10,
  ssl: true
}

// callback
MongoClient.connect(MongoDB_DB_URL, options, function(e, client) {

   if(e) throw new Error('Error while try to connect to MongoDB Database - error: ' + e);

   console.log( 'MongoDB - Connected successfully to server..' );
   myDB = client.db( MongoDB_DB_NAME );
   db.close();
});


// async
async function connectMongoDB(){
log('connectMongoDB()');

      try {
        const client = await MongoClient.connect(MongoDB_DB_URL, options);

        // create database handle / connect to database
        myDB = client.db(MongoDB_DB_NAME);

        // retrieve client options
        const clientOptions = client?.s?.options;

        // verify custom set options
        const timeout = clientOptions.connectTimeoutMS;

        // check for SSL
        // clientOptions.ssl; <-- should be true if SSL

        // get user
        // clientOptions.user;

        // check database user
        // clientOptions.authSource;

        log( 'Successfully connected to MongoDB Database' );
        db.close();
        return {code : "SUCCESS"};
      } catch (e) {
        log( chalk.red.bold('❌ ERROR') + ' Error while try to connect to MongoDB Database - ' + chalk.white.bold('error:\n') + e );
        return {code : "ERROR", e: e};
      }

};





/*
Option	Affects	Type	Default	Description
poolSize	Server, ReplicaSet, Mongos	integer	5	Set the maximum poolSize for each individual server or proxy connection.
ssl	Server, ReplicaSet, Mongos	boolean	false	Use ssl connection (needs to have a mongod server with ssl support)
sslValidate	Server, ReplicaSet, Mongos	boolean	true	Validate mongod server certificate against ca (needs to have a mongod server with ssl support, 2.4 or higher)
sslCA	Server, ReplicaSet, Mongos	Array	null	Array of valid certificates either as Buffers or Strings (needs to have a mongod server with ssl support, 2.4 or higher)
sslCert	Server, ReplicaSet, Mongos	Buffer/String	null	String or buffer containing the certificate we wish to present (needs to have a mongod server with ssl support, 2.4 or higher)
sslKey	Server, ReplicaSet, Mongos	Buffer/String	null	String or buffer containing the certificate private key we wish to present (needs to have a mongod server with ssl support, 2.4 or higher)
sslPass	Server, ReplicaSet, Mongos	Buffer/String	null	String or buffer containing the certificate password (needs to have a mongod server with ssl support, 2.4 or higher)
autoReconnect	Server	boolean	true	Reconnect on error.
noDelay	Server, ReplicaSet, Mongos	boolean	true	TCP Socket NoDelay option.
keepAlive	Server, ReplicaSet, Mongos	integer	0	The number of milliseconds to wait before initiating keepAlive on the TCP socket.
connectTimeoutMS	Server, ReplicaSet, Mongos	integer	30000	TCP Connection timeout setting.
socketTimeoutMS	Server, ReplicaSet, Mongos	integer	30000	TCP Socket timeout setting.
reconnectTries	Server	integer	30	Server attempt to reconnect #times
reconnectInterval	Server	integer	1000	Server will wait # milliseconds between retries.
ha	ReplicaSet, Mongos	boolean	true	Turn on high availability monitoring.
haInterval	ReplicaSet, Mongos	integer	10000,5000	Time between each replicaset status check.
replicaSet	ReplicaSet	string	null	The name of the replicaset to connect to.
secondaryAcceptableLatencyMS	ReplicaSet	integer	15	Sets the range of servers to pick when using NEAREST (lowest ping ms + the latency fence, ex: range of 1 to (1 + 15) ms).
acceptableLatencyMS	Mongos	integer	15	Sets the range of servers to pick when using NEAREST (lowest ping ms + the latency fence, ex: range of 1 to (1 + 15) ms).
connectWithNoPrimary	ReplicaSet	boolean	false	Sets if the driver should connect even if no primary is available.
authSource	Server, ReplicaSet, Mongos	string	null	If the database authentication is dependent on another databaseName.
w	Server, ReplicaSet, Mongos	string, integer	null	The write concern.
wtimeout	Server, ReplicaSet, Mongos	integer	null	The write concern timeout value.
j	Server, ReplicaSet, Mongos	boolean	false	Specify a journal write concern.
forceServerObjectId	Server, ReplicaSet, Mongos	boolean	false	Force server to assign _id values instead of driver.
serializeFunctions	Server, ReplicaSet, Mongos	boolean	false	Serialize functions on any object.
ignoreUndefined	Server, ReplicaSet, Mongos	boolean	false	Specify if the BSON serializer should ignore undefined fields.
raw	Server, ReplicaSet, Mongos	boolean	false	Return document results as raw BSON buffers.
promoteLongs	Server, ReplicaSet, Mongos	boolean	true	Promotes Long values to number if they fit inside the 53 bits resolution.
bufferMaxEntries	Server, ReplicaSet, Mongos	integer	-1	Sets a cap on how many operations the driver will buffer up before giving up on getting a working connection, default is -1 which is unlimited.
readPreference	Server, ReplicaSet, Mongos	object	null	The preferred read preference (ReadPreference.PRIMARY, ReadPreference.PRIMARY_PREFERRED, ReadPreference.SECONDARY, ReadPreference.SECONDARY_PREFERRED, ReadPreference.NEAREST).
pkFactory	Server, ReplicaSet, Mongos	object	null	A primary key factory object for generation of custom _id keys.
promiseLibrary	Server, ReplicaSet, Mongos	object	null	A Promise library class the application wishes to use such as Bluebird, must be ES6 compatible.
readConcern	Server, ReplicaSet, Mongos	object	null	Specify a read concern for the collection. (only MongoDB 3.2 or hig
*/
```

<br><br>

## Connection Pooling 
- Allows reusing Database Connections. For default you create a connection and then close it. With Connection Pooling you reuse the connection.
- Requests are faster and use less Hardware Resources
- Default size is 100























































<br><br>

____________________________________________________
____________________________________________________

<br><br>


# Atlas (https://www.mongodb.com/cloud/atlas)
- cloud database service

## Guides
- Setting Up Atlas (https://www.youtube.com/watch?v=xhAYGeZoZTk)

## Connect
- Method #1 - Limit access to IP. If you want to allow all then add 0.0.0.0/0
- Method #2 - Use username and password


## .env
```bash
# Ticket: Connection
# Rename this file to .env after filling in your MFLIX_DB_URI and your SECRET_KEY
# Do not surround the URI with quotes
SECRET_KEY=1234567887654321
MFLIX_DB_URI=mongodb+srv://username:password@mflix.ptrji.mongodb.net/test
MFLIX_NS=sample_mflix
PORT=5000
```














































<br><br>

____________________________________________________
____________________________________________________

<br><br>

# Operators

## Logical Query Operators

#### Comparison Query Operators (https://docs.mongodb.com/manual/reference/operator/query-comparison/)
- $eq	Matches values that are equal to a specified value. (https://docs.mongodb.com/manual/reference/operator/aggregation/eq/)
- $gt	Matches values that are greater than a specified value. (https://docs.mongodb.com/manual/reference/operator/aggregation/gt/)
- $gte	Matches values that are greater than or equal to a specified value. (https://docs.mongodb.com/manual/reference/operator/aggregation/gte/)
- $in	Matches any of the values specified in an array. (https://docs.mongodb.com/manual/reference/operator/aggregation/in/)
- $lt	Matches values that are less than a specified value. (https://docs.mongodb.com/manual/reference/operator/aggregation/lt/)
- $lte	Matches values that are less than or equal to a specified value. (https://docs.mongodb.com/manual/reference/operator/aggregation/lte/)
- $ne	Matches all values that are not equal to a specified value. (https://docs.mongodb.com/manual/reference/operator/aggregation/ne/)
- $nin	Matches none of the values specified in an array. (https://docs.mongodb.com/manual/reference/operator/query/nin/)

<br><br>

#### Logical Query Operators (https://docs.mongodb.com/manual/reference/operator/query-logical/)
- $and	Joins query clauses with a logical AND returns all documents that match the conditions of both clauses. (https://docs.mongodb.com/manual/reference/operator/query/and/)
- $not	Inverts the effect of a query expression and returns documents that do not match the query expression. (https://docs.mongodb.com/manual/reference/operator/query/not/)
- $nor	Joins query clauses with a logical NOR returns all documents that fail to match both clauses. (https://docs.mongodb.com/manual/reference/operator/query/nor/)
- $or	Joins query clauses with a logical OR returns all documents that match the conditions of either clause. (https://docs.mongodb.com/manual/reference/operator/query/or/)

<br><br>

#### Element Query Operators (https://docs.mongodb.com/manual/reference/operator/query-element/)
- $exists	Matches documents that have the specified field. (https://docs.mongodb.com/manual/reference/operator/query/exists/)
- $type	Selects documents if a field is of the specified type. (https://docs.mongodb.com/manual/reference/operator/query/type/)

<br><br>

#### Evaluation Query Operators (https://docs.mongodb.com/manual/reference/operator/query-evaluation/)
- $expr	Allows use of aggregation expressions within the query language. (https://docs.mongodb.com/manual/reference/operator/query/expr/)
- $jsonSchema	Validate documents against the given JSON Schema. (https://docs.mongodb.com/manual/reference/operator/query/jsonSchema/)
- $mod	Performs a modulo operation on the value of a field and selects documents with a specified result. (https://docs.mongodb.com/manual/reference/operator/query/mod/)
- $regex	Selects documents where values match a specified regular expression. (https://docs.mongodb.com/manual/reference/operator/query/regex/)
- $text	Performs text search. (https://docs.mongodb.com/manual/reference/operator/query/text/)
- $where	Matches documents that satisfy a JavaScript expression. (https://docs.mongodb.com/manual/reference/operator/query/where/)

<br><br>

#### Geospatial Query Operators (https://docs.mongodb.com/manual/reference/operator/query-geospatial/)
- $geoIntersects	Selects geometries that intersect with a GeoJSON geometry. The 2dsphere index supports $geoIntersects. (https://docs.mongodb.com/manual/reference/operator/query/geoIntersects/)
- $geoWithin	Selects geometries within a bounding GeoJSON geometry. The 2dsphere and 2d indexes support $geoWithin. (https://docs.mongodb.com/manual/reference/operator/query/geoWithin/)
- $near	Returns geospatial objects in proximity to a point. Requires a geospatial index. The 2dsphere and 2d indexes support $near. (https://docs.mongodb.com/manual/reference/operator/query/near/)
- $nearSphere	Returns geospatial objects in proximity to a point on a sphere. Requires a geospatial index. The 2dsphere and 2d indexes support $nearSphere. (https://docs.mongodb.com/manual/reference/operator/query/nearSphere/)


<br><br>

#### Array Query Operators (https://docs.mongodb.com/manual/reference/operator/query-array/)
- $all	Matches arrays that contain all elements specified in the query. (https://docs.mongodb.com/manual/reference/operator/query/all/)
- $elemMatch	Selects documents if element in the array field matches all the specified $elemMatch conditions. (https://docs.mongodb.com/manual/reference/operator/query/elemMatch/)
- $size	Selects documents if the array field is a specified size. (https://docs.mongodb.com/manual/reference/operator/query/size/)


<br><br>

#### Bitwise Query Operators (https://docs.mongodb.com/manual/reference/operator/query-bitwise/)
- $bitsAllClear	Matches numeric or binary values in which a set of bit positions all have a value of 0. (https://docs.mongodb.com/manual/reference/operator/query/bitsAllClear/)
- $bitsAllSet	Matches numeric or binary values in which a set of bit positions all have a value of 1. (https://docs.mongodb.com/manual/reference/operator/query/bitsAllSet/)
- $bitsAnyClear	Matches numeric or binary values in which any bit from a set of bit positions has a value of 0. (https://docs.mongodb.com/manual/reference/operator/query/bitsAnyClear/)
- $bitsAnySet	Matches numeric or binary values in which any bit from a set of bit positions has a value of 1. (https://docs.mongodb.com/manual/reference/operator/query/bitsAnySet/)










<br><br><br><br>


## Aggregation Pipeline Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/)




<br><br>

#### Aggregation Pipeline Stages
- $addFields	Adds new fields to documents. Similar to $project, $addFields reshapes each document in the stream; specifically, by adding new fields to output documents that contain both the existing fields from the input documents and the newly added fields. (https://docs.mongodb.com/manual/reference/operator/aggregation/addFields/#pipe._S_addFields)
- $bucket	Categorizes incoming documents into groups, called buckets, based on a specified expression and bucket boundaries. (https://docs.mongodb.com/manual/reference/operator/aggregation/bucket/#pipe._S_bucket)
- $bucketAuto	Categorizes incoming documents into a specific number of groups, called buckets, based on a specified expression. Bucket boundaries are automatically determined in an attempt to evenly distribute the documents into the specified number of buckets. (https://docs.mongodb.com/manual/reference/operator/aggregation/bucketAuto/#pipe._S_bucketAuto)
- $collStats	Returns statistics regarding a collection or view. (https://docs.mongodb.com/manual/reference/operator/aggregation/collStats/#pipe._S_collStats)
- $count	Returns a count of the number of documents at this stage of the aggregation pipeline. (https://docs.mongodb.com/manual/reference/operator/aggregation/count/#pipe._S_count)
- $facet	Processes multiple aggregation pipelines within a single stage on the same set of input documents. Enables the creation of multi-faceted aggregations capable of characterizing data across multiple dimensions, or facets, in a single stage. (https://docs.mongodb.com/manual/reference/operator/aggregation/facet/#pipe._S_facet)
- $geoNear	Returns an ordered stream of documents based on the proximity to a geospatial point. Incorporates the functionality of $match, $sort, and $limit for geospatial data. The output documents include an additional distance field and can include a location identifier field. (https://docs.mongodb.com/manual/reference/operator/aggregation/geoNear/#pipe._S_geoNear)
- $graphLookup	Performs a recursive search on a collection. To each output document, adds a new array field that contains the traversal results of the recursive search for that document. (https://docs.mongodb.com/manual/reference/operator/aggregation/graphLookup/#pipe._S_graphLookup)

<br><br>
- $group	Groups input documents by a specified identifier expression and applies the accumulator expression(s), if specified, to each group. Consumes all input documents and outputs one document per each distinct group. The output documents only contain the identifier field and, if specified, accumulated fields. (https://docs.mongodb.com/manual/reference/operator/aggregation/group/#pipe._S_group)
```javascript
/* Our collection looks like this:
{ "_id" : 1, "item" : "abc", "price" : 10, "quantity" : 2, "date" : ISODate("2014-01-01T08:00:00Z") }
{ "_id" : 2, "item" : "jkl", "price" : 20, "quantity" : 1, "date" : ISODate("2014-02-03T09:00:00Z") }
{ "_id" : 3, "item" : "xyz", "price" : 5, "quantity" : 5, "date" : ISODate("2014-02-03T09:05:00Z") }
{ "_id" : 4, "item" : "abc", "price" : 10, "quantity" : 10, "date" : ISODate("2014-02-15T08:00:00Z") }
{ "_id" : 5, "item" : "xyz", "price" : 5, "quantity" : 10, "date" : ISODate("2014-02-15T09:12:00Z") }
*/


const pipeline = [{$group: {
                 _id: "$item",
                avgAmount: { $avg: { $multiply: [ "$price", "$quantity" ] } },
                avgQuantity: { $avg: "$quantity" }
              }}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
{ "_id" : "xyz", "avgAmount" : 37.5, "avgQuantity" : 7.5 }
{ "_id" : "jkl", "avgAmount" : 20, "avgQuantity" : 1 }
{ "_id" : "abc", "avgAmount" : 60, "avgQuantity" : 6 }
*/
```
<br><br>


- $indexStats	Returns statistics regarding the use of each index for the collection. (https://docs.mongodb.com/manual/reference/operator/aggregation/indexStats/#pipe._S_indexStats)
- $limit	Passes the first n documents unmodified to the pipeline where n is the specified limit. For each input document, outputs either one document (for the first n documents) or zero documents (after the first n documents). (https://docs.mongodb.com/manual/reference/operator/aggregation/limit/#pipe._S_limit)
- $listSessions	Lists all sessions that have been active long enough to propagate to the system.sessions collection. (https://docs.mongodb.com/manual/reference/operator/aggregation/listSessions/#pipe._S_listSessions)
- $lookup	Performs a left outer join to another collection in the same database to filter in documents from the “joined” collection for processing. (https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/#pipe._S_lookup)

<br><br>

- $match	Filters the document stream to allow only matching documents to pass unmodified into the next pipeline stage. For each input document, outputs either one document (a match) or zero documents (no match). (https://docs.mongodb.com/manual/reference/operator/aggregation/match/#pipe._S_match)
- $match uses standard MongoDB Query Operators.
- We can not use $where
- If we use $text the $match stage must be the first.
- If $match is first stage it can take advantages of index and is faster.
- $match uses the same query syntax as find and you can compare it to filter from javascript.


<br><br>

- $merge	Writes the resulting documents of the aggregation pipeline to a collection. The stage can incorporate (insert new documents, merge documents, replace documents, keep existing documents, fail the operation, process documents with a custom update pipeline) the results into an output collection. To use the $merge stage, it must be the last stage in the pipeline. (https://docs.mongodb.com/manual/reference/operator/aggregation/merge/#pipe._S_merge)
- $out	Writes the resulting documents of the aggregation pipeline to a collection. To use the $out stage, it must be the last stage in the pipeline. (https://docs.mongodb.com/manual/reference/operator/aggregation/out/#pipe._S_out)
- $planCacheStats	Returns plan cache information for a collection. (https://docs.mongodb.com/manual/reference/operator/aggregation/planCacheStats/#pipe._S_planCacheStats)


<br><br>
- $project	Reshapes each document in the stream, such as by adding new fields or removing existing fields. For each input document, outputs one document. See also $unset for removing existing fields. (https://docs.mongodb.com/manual/reference/operator/aggregation/project/#pipe._S_project)
- You must manually specify each field which you want to return. Only **_id** field will be also returned! If you do not want this then use **{_id: 0}**
- You can compare it with .map from javascript.
- Can be used as many time as you want within aggregation pipeline.
```javascript
const pipeline = [{$project: {_id: 0, item: 1}}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});
```
<br><br>

- $redact	Reshapes each document in the stream by restricting the content for each document based on information stored in the documents themselves. Incorporates the functionality of $project and $match. Can be used to implement field level redaction. For each input document, outputs either one or zero documents. (https://docs.mongodb.com/manual/reference/operator/aggregation/redact/#pipe._S_redact)
- $replaceRoot	Replaces a document with the specified embedded document. The operation replaces all existing fields in the input document, including the _id field. Specify a document embedded in the input document to promote the embedded document to the top level. (https://docs.mongodb.com/manual/reference/operator/aggregation/replaceRoot/#pipe._S_replaceRoot)
- $replaceWith is an alias for $replaceRoot stage. Replaces a document with the specified embedded document. The operation replaces all existing fields in the input document, including the _id field. Specify a document embedded in the input document to promote the embedded document to the top level.
 $replaceWith is an alias for $replaceRoot stage.
- $sample	Randomly selects the specified number of documents from its input. (https://docs.mongodb.com/manual/reference/operator/aggregation/sample/#pipe._S_sample)
- $set	Adds new fields to documents. Similar to $project, $set reshapes each document in the stream; specifically, by adding new fields to output documents that contain both the existing fields from the input documents and the newly added fields.
- $set is an alias for $addFields stage. (https://docs.mongodb.com/manual/reference/operator/aggregation/set/#pipe._S_set)
- $skip	Skips the first n documents where n is the specified skip number and passes the remaining documents unmodified to the pipeline. For each input document, outputs either zero documents (for the first n documents) or one document (if after the first n documents). (https://docs.mongodb.com/manual/reference/operator/aggregation/skip/#pipe._S_skip)
- $sort	Reorders the document stream by a specified sort key. Only the order changes; the documents remain unmodified. For each input document, outputs one document. (https://docs.mongodb.com/manual/reference/operator/aggregation/sort/#pipe._S_sort)
- $sortByCount	Groups incoming documents based on the value of a specified expression, then computes the count of documents in each distinct group. (https://docs.mongodb.com/manual/reference/operator/aggregation/sortByCount/#pipe._S_sortByCount)
- $unionWith	Performs a union of two collections; i.e. combines pipeline results from two collections into a single result set. (https://docs.mongodb.com/manual/reference/operator/aggregation/unionWith/#pipe._S_unionWith)
- $unset	Removes/excludes fields from documents. $unset is an alias for $project stage that removes fields.(https://docs.mongodb.com/manual/reference/operator/aggregation/unset/#pipe._S_unset)
- $unwind	Deconstructs an array field from the input documents to output a document for each element. Each output document replaces the array with an element value. For each input document, outputs n documents where n is the number of array elements and can be zero for an empty array. (https://docs.mongodb.com/manual/reference/operator/aggregation/unwind/#pipe._S_unwind)





<br><br>



#### Alphabetical Listing of Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#alphabetical-listing-of-expression-operators)

<br><br>
<br><br>

#### Arithmetic Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#arithmetic-expression-operators)
- $abs	Returns the absolute value of a number. (https://docs.mongodb.com/manual/reference/operator/aggregation/abs/#exp._S_abs)

<br><br>
- $add	Adds numbers to return the sum, or adds numbers and a date to return a new date. If adding numbers and a date, treats the numbers as milliseconds. Accepts any number of argument expressions, but at most, one expression can resolve to a date. (https://docs.mongodb.com/manual/reference/operator/aggregation/add/#exp._S_add)
```javascript
// add price + fee
const pipeline = [{$project: {item: 1, total: {$add: [ "$price", "$fee" ]}}}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});
```

<br><br>

- $ceil	Returns the smallest integer greater than or equal to the specified number. (https://docs.mongodb.com/manual/reference/operator/aggregation/ceil/#exp._S_ceil)

<br><br>
- $divide	Returns the result of dividing the first number by the second. Accepts two argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/divide/#exp._S_divide)
```javascript
/* our collection looks like this:
{ "_id" : 1, "item" : "abc", "price" : 10, "discount": 2, date: ISODate("2014-03-01T08:00:00Z") }
{ "_id" : 2, "item" : "jkl", "price" : 20, "discount": 2, date: ISODate("2014-03-01T09:00:00Z") }
{ "_id" : 3, "item" : "xyz", "price" : 5, "discount": 2, date: ISODate("2014-03-15T09:00:00Z") }
*/

// add price + fee
const pipeline = [
  {$project: {date: 1, item: 1, newPrice: {$divide: ["$price", "$discount"]}}}
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
The operation returns the following results:
{ "_id" : 1, "item" : "abc", "date" : ISODate("2014-03-01T08:00:00Z"), "newPrice" : 5 }
{ "_id" : 2, "item" : "jkl", "date" : ISODate("2014-03-01T09:00:00Z"), "newPrice" : 10 }
{ "_id" : 3, "item" : "xyz", "date" : ISODate("2014-03-15T09:00:00Z"), "newPrice" : 2.5 }
*/
```
<br><br>


- $exp	Raises e to the specified exponent. (https://docs.mongodb.com/manual/reference/operator/aggregation/exp/#exp._S_exp)
- $floor	Returns the largest integer less than or equal to the specified number. (https://docs.mongodb.com/manual/reference/operator/aggregation/floor/#exp._S_floor)
- $ln	Calculates the natural log of a number. (https://docs.mongodb.com/manual/reference/operator/aggregation/ln/#exp._S_ln)
- $log	Calculates the log of a number in the specified base. (https://docs.mongodb.com/manual/reference/operator/aggregation/log/#exp._S_log)
- $log10	Calculates the log base 10 of a number. (https://docs.mongodb.com/manual/reference/operator/aggregation/log10/#exp._S_log10)
- $mod	Returns the remainder of the first number divided by the second. Accepts two argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/mod/#exp._S_mod)

<br><br>
- $multiply	Multiplies numbers to return the product. Accepts any number of argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/multiply/#exp._S_multiply)
```javascript
/* our collection looks like this:
{ "_id" : 1, "item" : "abc", "price" : 10, "quantity": 2, date: ISODate("2014-03-01T08:00:00Z") }
{ "_id" : 2, "item" : "jkl", "price" : 20, "quantity": 1, date: ISODate("2014-03-01T09:00:00Z") }
{ "_id" : 3, "item" : "xyz", "price" : 5, "quantity": 10, date: ISODate("2014-03-15T09:00:00Z") }
*/

// add price + fee
const pipeline = [
     {$project: {date: 1, item: 1, total: {$multiply: [ "$price", "$quantity" ]}}}
   ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
The operation returns the following results:
{ "_id" : 1, "item" : "abc", "date" : ISODate("2014-03-01T08:00:00Z"), "total" : 20 }
{ "_id" : 2, "item" : "jkl", "date" : ISODate("2014-03-01T09:00:00Z"), "total" : 20 }
{ "_id" : 3, "item" : "xyz", "date" : ISODate("2014-03-15T09:00:00Z"), "total" : 50 }
*/
```
<br><br>

- $pow	Raises a number to the specified exponent. (https://docs.mongodb.com/manual/reference/operator/aggregation/pow/#exp._S_pow)
- $round	Rounds a number to to a whole integer or to a specified decimal place. (https://docs.mongodb.com/manual/reference/operator/aggregation/round/#exp._S_round)
- $sqrt	Calculates the square root. (https://docs.mongodb.com/manual/reference/operator/aggregation/sqrt/#exp._S_sqrt)
- $subtract	Returns the result of subtracting the second value from the first. If the two values are numbers, return the difference. If the two values are dates, return the difference in milliseconds. If the two values are a date and a number in milliseconds, return the resulting date. Accepts two argument expressions. If the two values are a date and a number, specify the date argument first as it is not meaningful to subtract a date from a number. (https://docs.mongodb.com/manual/reference/operator/aggregation/subtract/#exp._S_subtract)
- $trunc	Truncates a number to a whole integer or to a specified decimal place. (https://docs.mongodb.com/manual/reference/operator/aggregation/trunc/#exp._S_trunc)

<br><br>

#### Array Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#array-expression-operators)
- $arrayElemAt	Returns the element at the specified array index. (https://docs.mongodb.com/manual/reference/operator/aggregation/arrayElemAt/#exp._S_arrayElemAt)
- $arrayToObject	Converts an array of key value pairs to a document. (https://docs.mongodb.com/manual/reference/operator/aggregation/arrayToObject/#exp._S_arrayToObject)
- $concatArrays	Concatenates arrays to return the concatenated array. (https://docs.mongodb.com/manual/reference/operator/aggregation/concatArrays/#exp._S_concatArrays)
- $filter	Selects a subset of the array to return an array with only the elements that match the filter condition. (https://docs.mongodb.com/manual/reference/operator/aggregation/filter/#exp._S_filter)
- $first	Returns the first array element. Distinct from $first accumulator. (https://docs.mongodb.com/manual/reference/operator/aggregation/first-array-element/#exp._S_first)
- $in	Returns a boolean indicating whether a specified value is in an array. (https://docs.mongodb.com/manual/reference/operator/aggregation/in/#exp._S_in)
- $indexOfArray	Searches an array for an occurrence of a specified value and returns the array index of the first occurrence. If the substring is not found, returns -1. (https://docs.mongodb.com/manual/reference/operator/aggregation/indexOfArray/#exp._S_indexOfArray)
- $isArray	Determines if the operand is an array. Returns a boolean. (https://docs.mongodb.com/manual/reference/operator/aggregation/isArray/#exp._S_isArray)
- $last	Returns the last array element. Distinct from $last accumulator. (https://docs.mongodb.com/manual/reference/operator/aggregation/last-array-element/#exp._S_last)
- $map	Applies a subexpression to each element of an array and returns the array of resulting values in order. Accepts named parameters. (https://docs.mongodb.com/manual/reference/operator/aggregation/map/#exp._S_map)
- $objectToArray	Converts a document to an array of documents representing key-value pairs. (https://docs.mongodb.com/manual/reference/operator/aggregation/objectToArray/#exp._S_objectToArray)
- $range	Outputs an array containing a sequence of integers according to user-defined inputs. (https://docs.mongodb.com/manual/reference/operator/aggregation/range/#exp._S_range)
- $reduce	Applies an expression to each element in an array and combines them into a single value. (https://docs.mongodb.com/manual/reference/operator/aggregation/reduce/#exp._S_reduce)
- $reverseArray	Returns an array with the elements in reverse order. (https://docs.mongodb.com/manual/reference/operator/aggregation/reverseArray/#exp._S_reverseArray)
- $size	Returns the number of elements in the array. Accepts a single expression as argument. (https://docs.mongodb.com/manual/reference/operator/aggregation/size/#exp._S_size)
- $slice	Returns a subset of an array. (https://docs.mongodb.com/manual/reference/operator/aggregation/slice/#exp._S_slice)
- $zip	Merge two arrays together. (https://docs.mongodb.com/manual/reference/operator/aggregation/zip/#exp._S_zip)

<br><br>

#### Boolean Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#boolean-expression-operators)
- $and	Returns true only when all its expressions evaluate to true. Accepts any number of argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/and/#exp._S_and)
- $not	Returns the boolean value that is the opposite of its argument expression. Accepts a single argument expression. (https://docs.mongodb.com/manual/reference/operator/aggregation/not/#exp._S_not)
- $or	Returns true when any of its expressions evaluates to true. Accepts any number of argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/or/#exp._S_or)


<br><br>

#### Comparison Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#comparison-expression-operators)
- $cmp	Returns 0 if the two values are equivalent, 1 if the first value is greater than the second, and -1 if the first value is less than the second. (https://docs.mongodb.com/manual/reference/operator/aggregation/cmp/#exp._S_cmp)
- $eq	Returns true if the values are equivalent. (https://docs.mongodb.com/manual/reference/operator/aggregation/eq/#exp._S_eq)
- $gt	Returns true if the first value is greater than the second. (https://docs.mongodb.com/manual/reference/operator/aggregation/gt/#exp._S_gt)
- $gte	Returns true if the first value is greater than or equal to the second. (https://docs.mongodb.com/manual/reference/operator/aggregation/gte/#exp._S_gte)
- $lt	Returns true if the first value is less than the second. (https://docs.mongodb.com/manual/reference/operator/aggregation/lt/#exp._S_lt)
- $lte	Returns true if the first value is less than or equal to the second. (https://docs.mongodb.com/manual/reference/operator/aggregation/lte/#exp._S_lte)
- $ne	Returns true if the values are not equivalent. (https://docs.mongodb.com/manual/reference/operator/aggregation/ne/#exp._S_ne)


<br><br>


#### Conditional Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#conditional-expression-operators)
- $cond	A ternary operator that evaluates one expression, and depending on the result, returns the value of one of the other two expressions. Accepts either three expressions in an ordered list or three named parameters. (https://docs.mongodb.com/manual/reference/operator/aggregation/cond/#exp._S_cond)
- $ifNull	Returns either the non-null result of the first expression or the result of the second expression if the first expression results in a null result. Null result encompasses instances of undefined values or missing fields. Accepts two expressions as arguments. The result of the second expression can be null. (https://docs.mongodb.com/manual/reference/operator/aggregation/ifNull/#exp._S_ifNull)
- $switch	Evaluates a series of case expressions. When it finds an expression which evaluates to true, $switch executes a specified expression and breaks out of the control flow. (https://docs.mongodb.com/manual/reference/operator/aggregation/switch/#exp._S_switch)



<br><br>

#### Custom Aggregation Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#custom-aggregation-expression-operators)
- $accumulator - Defines a custom accumulator function. (https://docs.mongodb.com/manual/reference/operator/aggregation/accumulator/#grp._S_accumulator)
- $function	- Defines a custom function. (https://docs.mongodb.com/manual/reference/operator/aggregation/function/#exp._S_function)



<br><br>

#### Data Size Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#data-size-operators)
- $binarySize	Returns the size of a given string or binary data value’s content in bytes. (https://docs.mongodb.com/manual/reference/operator/aggregation/binarySize/#exp._S_binarySize)
- $bsonSize	Returns the size in bytes of a given document (i.e. bsontype Object) when encoded as BSON. (https://docs.mongodb.com/manual/reference/operator/aggregation/bsonSize/#exp._S_bsonSize)




<br><br>

#### Date Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#date-expression-operators)
- $dateFromParts	Constructs a BSON Date object given the date’s constituent parts. (https://docs.mongodb.com/manual/reference/operator/aggregation/dateFromParts/#exp._S_dateFromParts)
- $dateFromString	Converts a date/time string to a date object. (https://docs.mongodb.com/manual/reference/operator/aggregation/dateFromString/#exp._S_dateFromString)
- $dateToParts	Returns a document containing the constituent parts of a date. (https://docs.mongodb.com/manual/reference/operator/aggregation/dateToParts/#exp._S_dateToParts)
- $dateToString	Returns the date as a formatted string. (https://docs.mongodb.com/manual/reference/operator/aggregation/dateToString/#exp._S_dateToString)
- $dayOfMonth	Returns the day of the month for a date as a number between 1 and 31. (https://docs.mongodb.com/manual/reference/operator/aggregation/dayOfMonth/#exp._S_dayOfMonth)
- $dayOfWeek	Returns the day of the week for a date as a number between 1 (Sunday) and 7 (Saturday). (https://docs.mongodb.com/manual/reference/operator/aggregation/dayOfWeek/#exp._S_dayOfWeek)
- $dayOfYear	Returns the day of the year for a date as a number between 1 and 366 (leap year). (https://docs.mongodb.com/manual/reference/operator/aggregation/dayOfYear/#exp._S_dayOfYear)
- $hour	Returns the hour for a date as a number between 0 and 23. (https://docs.mongodb.com/manual/reference/operator/aggregation/hour/#exp._S_hour)
- $isoDayOfWeek	Returns the weekday number in ISO 8601 format, ranging from 1 (for Monday) to 7 (for Sunday). (https://docs.mongodb.com/manual/reference/operator/aggregation/isoDayOfWeek/#exp._S_isoDayOfWeek)
- $isoWeek	Returns the week number in ISO 8601 format, ranging from 1 to 53. Week numbers start at 1 with the week (Monday through Sunday) that contains the year’s first Thursday. (https://docs.mongodb.com/manual/reference/operator/aggregation/isoWeek/#exp._S_isoWeek)
- $isoWeekYear	Returns the year number in ISO 8601 format. The year starts with the Monday of week 1 (ISO 8601) and ends with the Sunday of the last week (ISO 8601). (https://docs.mongodb.com/manual/reference/operator/aggregation/isoWeekYear/#exp._S_isoWeekYear)
- $millisecond	Returns the milliseconds of a date as a number between 0 and 999. (https://docs.mongodb.com/manual/reference/operator/aggregation/millisecond/#exp._S_millisecond)
- $minute	Returns the minute for a date as a number between 0 and 59. (https://docs.mongodb.com/manual/reference/operator/aggregation/minute/#exp._S_minute)
- $month	Returns the month for a date as a number between 1 (January) and 12 (December). (https://docs.mongodb.com/manual/reference/operator/aggregation/month/#exp._S_month)
- $second	Returns the seconds for a date as a number between 0 and 60 (leap seconds). (https://docs.mongodb.com/manual/reference/operator/aggregation/second/#exp._S_second)
- $toDate	Converts value to a Date. (https://docs.mongodb.com/manual/reference/operator/aggregation/toDate/#exp._S_toDate)
- $week	Returns the week number for a date as a number between 0 (the partial week that precedes the first Sunday of the year) and 53 (leap year). (https://docs.mongodb.com/manual/reference/operator/aggregation/week/#exp._S_week)
- $year	Returns the year for a date as a number (e.g. 2014). (https://docs.mongodb.com/manual/reference/operator/aggregation/year/#exp._S_year)
- $add	Adds numbers and a date to return a new date. If adding numbers and a date, treats the numbers as milliseconds. Accepts any number of argument expressions, but at most, one expression can resolve to a date. (https://docs.mongodb.com/manual/reference/operator/aggregation/add/#exp._S_add)
- $subtract	Returns the result of subtracting the second value from the first. If the two values are dates, return the difference in milliseconds. If the two values are a date and a number in milliseconds, return the resulting date. Accepts two argument expressions. If the two values are a date and a number, specify the date argument first as it is not meaningful to subtract a date from a number. (https://docs.mongodb.com/manual/reference/operator/aggregation/subtract/#exp._S_subtract)




<br><br>

#### Literal Expression Operator (https://docs.mongodb.com/manual/reference/operator/aggregation/#literal-expression-operator)
- $literal	Return a value without parsing. Use for values that the aggregation pipeline may interpret as an expression. For example, use a $literal expression to a string that starts with a $ to avoid parsing as a field path. (https://docs.mongodb.com/manual/reference/operator/aggregation/literal/#exp._S_literal)



<br><br>

#### Miscellaneous Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#miscellaneous-operators)
- $rand	Returns a random float between 0 and 1 (https://docs.mongodb.com/manual/reference/operator/aggregation/rand/#exp._S_rand)
- $sampleRate	Randomly select documents at a given rate. Although the exact number of documents selected varies on each run, the quantity chosen approximates the sample rate expressed as a percentage of the total number of documents. (https://docs.mongodb.com/manual/reference/operator/aggregation/sampleRate/#exp._S_sampleRate)



<br><br>

#### Object Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#object-expression-operators)
- $mergeObjects	Combines multiple documents into a single document. (https://docs.mongodb.com/manual/reference/operator/aggregation/mergeObjects/#exp._S_mergeObjects)
- $objectToArray	Converts a document to an array of documents representing key-value pairs. (https://docs.mongodb.com/manual/reference/operator/aggregation/objectToArray/#exp._S_objectToArray)


<br><br>

#### Set Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#set-expression-operators)
- $allElementsTrue	Returns true if no element of a set evaluates to false, otherwise, returns false. Accepts a single argument expression. (https://docs.mongodb.com/manual/reference/operator/aggregation/allElementsTrue/#exp._S_allElementsTrue)
- $anyElementTrue	Returns true if any elements of a set evaluate to true; otherwise, returns false. Accepts a single argument expression. (https://docs.mongodb.com/manual/reference/operator/aggregation/anyElementTrue/#exp._S_anyElementTrue)
- $setDifference	Returns a set with elements that appear in the first set but not in the second set; i.e. performs a relative complement of the second set relative to the first. Accepts exactly two argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/setDifference/#exp._S_setDifference)
- $setEquals	Returns true if the input sets have the same distinct elements. Accepts two or more argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/setEquals/#exp._S_setEquals)
- $setIntersection	Returns a set with elements that appear in all of the input sets. Accepts any number of argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/setIntersection/#exp._S_setIntersection)
- $setIsSubset	Returns true if all elements of the first set appear in the second set, including when the first set equals the second set; i.e. not a strict subset. Accepts exactly two argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/setIsSubset/#exp._S_setIsSubset)
- $setUnion	Returns a set with elements that appear in any of the input sets. (https://docs.mongodb.com/manual/reference/operator/aggregation/setUnion/#exp._S_setUnion)

<br><br>

#### String Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#string-expression-operators)
- $concat	Concatenates any number of strings. (https://docs.mongodb.com/manual/reference/operator/aggregation/concat/#exp._S_concat)
- $dateFromString	Converts a date/time string to a date object. (https://docs.mongodb.com/manual/reference/operator/aggregation/dateFromString/#exp._S_dateFromString)
- $dateToString	Returns the date as a formatted string. (https://docs.mongodb.com/manual/reference/operator/aggregation/dateToString/#exp._S_dateToString)
- $indexOfBytes	Searches a string for an occurrence of a substring and returns the UTF-8 byte index of the first occurrence. If the substring is not found, returns -1. (https://docs.mongodb.com/manual/reference/operator/aggregation/indexOfBytes/#exp._S_indexOfBytes)
- $indexOfCP	Searches a string for an occurrence of a substring and returns the UTF-8 code point index of the first occurrence. If the substring is not found, returns -1 (https://docs.mongodb.com/manual/reference/operator/aggregation/indexOfCP/#exp._S_indexOfCP)
- $ltrim	Removes whitespace or the specified characters from the beginning of a string. (https://docs.mongodb.com/manual/reference/operator/aggregation/ltrim/#exp._S_ltrim)
- $regexFind	Applies a regular expression (regex) to a string and returns information on the first matched substring. (https://docs.mongodb.com/manual/reference/operator/aggregation/regexFind/#exp._S_regexFind)
- $regexFindAll	Applies a regular expression (regex) to a string and returns information on the all matched substrings. (https://docs.mongodb.com/manual/reference/operator/aggregation/regexFindAll/#exp._S_regexFindAll)
- $regexMatch	Applies a regular expression (regex) to a string and returns a boolean that indicates if a match is found or not. (https://docs.mongodb.com/manual/reference/operator/aggregation/regexMatch/#exp._S_regexMatch)
- $replaceOne	Replaces the first instance of a matched string in a given input. (https://docs.mongodb.com/manual/reference/operator/aggregation/replaceOne/#exp._S_replaceOne)
- $replaceAll	Replaces all instances of a matched string in a given input. (https://docs.mongodb.com/manual/reference/operator/aggregation/replaceAll/#exp._S_replaceAll)
- $rtrim	Removes whitespace or the specified characters from the end of a string. (https://docs.mongodb.com/manual/reference/operator/aggregation/rtrim/#exp._S_rtrim)
- $split	Splits a string into substrings based on a delimiter. Returns an array of substrings. If the delimiter is not found within the string, returns an array containing the original string. (https://docs.mongodb.com/manual/reference/operator/aggregation/split/#exp._S_split)
- $strLenBytes	Returns the number of UTF-8 encoded bytes in a string. (https://docs.mongodb.com/manual/reference/operator/aggregation/strLenBytes/#exp._S_strLenBytes)
- $strLenCP	Returns the number of UTF-8 code points in a string. (https://docs.mongodb.com/manual/reference/operator/aggregation/strLenCP/#exp._S_strLenCP)
- $strcasecmp	Performs case-insensitive string comparison and returns: 0 if two strings are equivalent, 1 if the first string is greater than the second, and -1 if the first string is less than the second. (https://docs.mongodb.com/manual/reference/operator/aggregation/strcasecmp/#exp._S_strcasecmp)
- $substr	Deprecated. Use $substrBytes or $substrCP. (https://docs.mongodb.com/manual/reference/operator/aggregation/substr/#exp._S_substr)
- $substrBytes	Returns the substring of a string. Starts with the character at the specified UTF-8 byte index (zero-based) in the string and continues for the specified number of bytes. (https://docs.mongodb.com/manual/reference/operator/aggregation/substrBytes/#exp._S_substrBytes)
- $substrCP	Returns the substring of a string. Starts with the character at the specified UTF-8 code point (CP) index (zero-based) in the string and continues for the number of code points specified. (https://docs.mongodb.com/manual/reference/operator/aggregation/substrCP/#exp._S_substrCP)
- $toLower	Converts a string to lowercase. Accepts a single argument expression. (https://docs.mongodb.com/manual/reference/operator/aggregation/toLower/#exp._S_toLower)
- $toString	Converts value to a string. (https://docs.mongodb.com/manual/reference/operator/aggregation/toString/#exp._S_toString)
- $trim	Removes whitespace or the specified characters from the beginning and end of a string. (https://docs.mongodb.com/manual/reference/operator/aggregation/trim/#exp._S_trim)
- $toUpper	Converts a string to uppercase. Accepts a single argument expression. (https://docs.mongodb.com/manual/reference/operator/aggregation/toUpper/#exp._S_toUpper)


<br><br>

#### Text Expression Operator (https://docs.mongodb.com/manual/reference/operator/aggregation/#text-expression-operator)
- $meta	Access available per-document metadata related to the aggregation operation. (https://docs.mongodb.com/manual/reference/operator/aggregation/meta/#exp._S_meta)



<br><br>

#### Trigonometry Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#trigonometry-expression-operators)
- $sin	Returns the sine of a value that is measured in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/sin/#exp._S_sin)
- $cos	Returns the cosine of a value that is measured in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/cos/#exp._S_cos)
- $tan	Returns the tangent of a value that is measured in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/tan/#exp._S_tan)
- $asin	Returns the inverse sin (arc sine) of a value in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/asin/#exp._S_asin)
- $acos	Returns the inverse cosine (arc cosine) of a value in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/acos/#exp._S_acos)
- $atan	Returns the inverse tangent (arc tangent) of a value in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/atan/#exp._S_atan)
- $atan2	Returns the inverse tangent (arc tangent) of y / x in radians, where y and x are the first and second values passed to the expression respectively. (https://docs.mongodb.com/manual/reference/operator/aggregation/atan2/#exp._S_atan2)
- $asinh	Returns the inverse hyperbolic sine (hyperbolic arc sine) of a value in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/asinh/#exp._S_asinh)
- $acosh	Returns the inverse hyperbolic cosine (hyperbolic arc cosine) of a value in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/acosh/#exp._S_acosh)
- $atanh	Returns the inverse hyperbolic tangent (hyperbolic arc tangent) of a value in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/atanh/#exp._S_atanh)
- $sinh	Returns the hyperbolic sine of a value that is measured in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/sinh/#exp._S_sinh)
- $cosh	Returns the hyperbolic cosine of a value that is measured in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/cosh/#exp._S_cosh)
- $tanh	Returns the hyperbolic tangent of a value that is measured in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/tanh/#exp._S_tanh)
- $degreesToRadians	Converts a value from degrees to radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/degreesToRadians/#exp._S_degreesToRadians)
- $radiansToDegrees	Converts a value from radians to degrees. (https://docs.mongodb.com/manual/reference/operator/aggregation/radiansToDegrees/#exp._S_radiansToDegrees)


<br><br>

#### Type Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#type-expression-operators)
- $convert	Converts a value to a specified type. (https://docs.mongodb.com/manual/reference/operator/aggregation/convert/#exp._S_convert)
- $isNumber	Returns boolean true if the specified expression resolves to an integer, decimal, double, or long. Returns boolean false if the expression resolves to any other BSON type, null, or a missing field. (https://docs.mongodb.com/manual/reference/operator/aggregation/isNumber/#exp._S_isNumber)
- $toBool	Converts value to a boolean. (https://docs.mongodb.com/manual/reference/operator/aggregation/toBool/#exp._S_toBool)
- $toDate	Converts value to a Date. (https://docs.mongodb.com/manual/reference/operator/aggregation/toDate/#exp._S_toDate)
- $toDecimal	Converts value to a Decimal128. (https://docs.mongodb.com/manual/reference/operator/aggregation/toDecimal/#exp._S_toDecimal)
- $toDouble	Converts value to a double. (https://docs.mongodb.com/manual/reference/operator/aggregation/toDouble/#exp._S_toDouble)
- $toInt	Converts value to an integer. (https://docs.mongodb.com/manual/reference/operator/aggregation/toInt/#exp._S_toInt)
- $toLong	Converts value to a long. (https://docs.mongodb.com/manual/reference/operator/aggregation/toLong/#exp._S_toLong)
- $toObjectId	Converts value to an ObjectId. (https://docs.mongodb.com/manual/reference/operator/aggregation/toObjectId/#exp._S_toObjectId)
- $toString	Converts value to a string. (https://docs.mongodb.com/manual/reference/operator/aggregation/toString/#exp._S_toString)
- $type	Return the BSON data type of the field. (https://docs.mongodb.com/manual/reference/operator/aggregation/type/#exp._S_type)




<br><br>

#### Accumulators ($group) (https://docs.mongodb.com/manual/reference/operator/aggregation/#accumulators-group)
- https://docs.mongodb.com/manual/reference/operator/aggregation/group/#pipe._S_group

<br><br>
- $accumulator	Returns the result of a user-defined accumulator function. (https://docs.mongodb.com/manual/reference/operator/aggregation/accumulator/#grp._S_accumulator)
- $addToSet	Returns an array of unique expression values for each group. Order of the array elements is undefined. (https://docs.mongodb.com/manual/reference/operator/aggregation/addToSet/#grp._S_addToSet)
- $avg	Returns an average of numerical values. Ignores non-numeric values. (https://docs.mongodb.com/manual/reference/operator/aggregation/avg/#grp._S_avg)
- $first	Returns a value from the first document for each group. Order is only defined if the documents are in a defined order. Distinct from the $first array operator. (https://docs.mongodb.com/manual/reference/operator/aggregation/first/#grp._S_first)
- $last	Returns a value from the last document for each group. Order is only defined if the documents are in a defined order. Distinct from the $last array operator. (https://docs.mongodb.com/manual/reference/operator/aggregation/last/#grp._S_last)
- $max	Returns the highest expression value for each group. (https://docs.mongodb.com/manual/reference/operator/aggregation/max/#grp._S_max)
- $mergeObjects	Returns a document created by combining the input documents for each group. (https://docs.mongodb.com/manual/reference/operator/aggregation/mergeObjects/#exp._S_mergeObjects)
- $min	Returns the lowest expression value for each group. (https://docs.mongodb.com/manual/reference/operator/aggregation/min/#grp._S_min)
- $push	Returns an array of expression values for each group. (https://docs.mongodb.com/manual/reference/operator/aggregation/push/#grp._S_push)
- $stdDevPop	Returns the population standard deviation of the input values. (https://docs.mongodb.com/manual/reference/operator/aggregation/stdDevPop/#grp._S_stdDevPop)
- $stdDevSamp	Returns the sample standard deviation of the input values. (https://docs.mongodb.com/manual/reference/operator/aggregation/stdDevSamp/#grp._S_stdDevSamp)
- $sum	Returns a sum of numerical values. Ignores non-numeric values. (https://docs.mongodb.com/manual/reference/operator/aggregation/sum/#grp._S_sum)





<br><br>

#### Accumulators (in Other Stages)
- $avg	Returns an average of the specified expression or list of expressions for each document. Ignores non-numeric values. (https://docs.mongodb.com/manual/reference/operator/aggregation/avg/#grp._S_avg)
- $max	Returns the maximum of the specified expression or list of expressions for each document (https://docs.mongodb.com/manual/reference/operator/aggregation/max/#grp._S_max)
- $min	Returns the minimum of the specified expression or list of expressions for each document (https://docs.mongodb.com/manual/reference/operator/aggregation/min/#grp._S_min)
- $stdDevPop	Returns the population standard deviation of the input values. (https://docs.mongodb.com/manual/reference/operator/aggregation/stdDevPop/#grp._S_stdDevPop)
- $stdDevSamp	Returns the sample standard deviation of the input values. (https://docs.mongodb.com/manual/reference/operator/aggregation/stdDevSamp/#grp._S_stdDevSamp)
- $sum	Returns a sum of numerical values. Ignores non-numeric values. (https://docs.mongodb.com/manual/reference/operator/aggregation/sum/#grp._S_sum)





<br><br>

#### Variable Expression Operators
- $let	Defines variables for use within the scope of a subexpression and returns the result of the subexpression. Accepts named parameters. Accepts any number of argument expressions.




























































































































































<br><br>
____________________________________________________
____________________________________________________

<br><br>


# create database handler
```javascript
const myDB = client.db(MongoDB_DB_NAME);
```


# create collection handler
```javascript
const myDB = client.db(MongoDB_DB_NAME);
const movies = myDB.collection('movies');
```

































<br><br>
____________________________________________________
____________________________________________________

<br><br>


# listCollections
- List all collections from Database
```javascript
const myDB = client.db(MongoDB_DB_NAME);
const collections = await myDB.listCollections().toArray();
```































<br><br>
____________________________________________________
____________________________________________________

<br><br>


# count Documents
- count all documents from collection
```javascript
// method #1 - .countDocuments (https://docs.mongodb.com/manual/reference/method/db.collection.countDocuments/#db.collection.countDocuments)
const numMovies = await movies.countDocuments({});

// method #2 - .count (https://docs.mongodb.com/manual/reference/method/db.collection.count/)
const numMovies = await movies.count({});

// method #3 - using operator
const numMovies = await movies.count({type: {$ne: 'Star'}});
```



































<br><br>

____________________________________________________
____________________________________________________

<br><br>


## dot notation (https://youtu.be/dpr_2cbC4Yk?t=191)
```javascript
/*
In our document in our collection we would have an "imdb" object which is nested and contains rating key. So as example:
const imdb = {"rating": 10};
*/
const query = [
{$match: {used: 0}},
{$project: {'imdb.rating': 1}},
];

// callback
collection.aggregate(query).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(query).toArray({});
```


































<br><br>

____________________________________________________
____________________________________________________

<br><br>


# Find Data



<br><br>

## read concern (https://docs.mongodb.com/manual/reference/read-concern/)
- The readConcern option allows you to control the consistency and isolation properties of the data read from replica sets and replica set shards.
- If you want to read important data like account details, bank balance or stuff like that you should not use **local**. Instead you should use a higher isolation like as example **majority** to double check your read process.

#### local (https://docs.mongodb.com/manual/reference/read-concern-local/#readconcern.%22local%22)
- The default read concern will be always local and will be perfomaned on the primary node.
- reads against secondaries if the reads are associated with causally consistent sessions.
- It **does not** check that data has been replicated

<br><br>

#### available (https://docs.mongodb.com/manual/reference/read-concern-available/#readconcern.%22available%22)
- The query returns data from the instance with no guarantee that the data has been written to a majority of the replica set members (i.e. may be rolled back).

<br><br>

#### majority (https://docs.mongodb.com/manual/reference/read-concern-majority/#readconcern.%22majority%22)
- The query returns the data that has been acknowledged by a majority of the replica set members. The documents returned by the read operation are durable, even in the event of failure.
- In easy words we will double check if the data exist on primary and secondary node.
- This will only returns data that has been replicated.

<br><br>

#### linearizable (https://docs.mongodb.com/manual/reference/read-concern-linearizable/#readconcern.%22linearizable%22)
- The query returns data that reflects all successful majority-acknowledged writes that completed prior to the start of the read operation. The query may wait for concurrently executing writes to propagate to a majority of replica set members before returning results.

<br><br>

#### snapshot (https://docs.mongodb.com/manual/reference/read-concern-snapshot/#readconcern.%22snapshot%22)
- If the transaction is not part of a causally consistent session, upon transaction commit with write concern "majority", the transaction operations are guaranteed to have read from a snapshot of majority-committed data.

```javascript
// callback
collection.deleteOne(pipeline, {readConcern: { level: 'majority' }}, function(e, result) {/* .. */ });

//async
const r = await comments.aggregate(pipeline, {readConcern: { level: 'majority' }});
```


<br><br>
<br><br>


#### Guides
- https://www.youtube.com/watch?v=G2fP0J571zo



<br><br>





#### pretty the result (https://docs.mongodb.com/manual/reference/method/cursor.pretty/)
```javascript
const query = {"id": msg.room};

// async
const r = await collection.findOne(query).pretty();

/*
{
    "_id" : ObjectId("54f612b6029b47909a90ce8d"),
    "title" : "A Tale of Two Cities",
    "text" : "It was the best of times, it was the worst of times, it was the age of wisdom, it was the age of foolishness...",
    "authorship" : "Charles Dickens"
}
*/
```








<br><br><br><br>


## .findOne

#### find specific item
```javascript
// callback
collection.findOne( {"id": msg.room}, (e, docs) => { /* .. */ });

// promise
collection
  .findOne({"title": "any title"})
  .then(doc => {
    const title = doc.title;
    // do something..
   })
   .catch(e => {
    console.log('error: ' + e);
  });


// async
const match = await collection.findOne({"title": "any title"});
console.log(match.title);

// or directly access the title
const {title} = await collection.findOne({"title": "any title"});
```


<br><br>


#### find specific item and specify the result (projection)
- By default, queries in MongoDB return all fields in matching documents. To limit the amount of data that MongoDB sends to applications, you can include a projection document to specify or restrict fields to return.
- 1 means true and 0 means false
```javascript
// method #1
const query = [
{title: "any title"},
{projection: {title: 1, year: 1}},
]

// method #2
const query = [
{title: "any title"},
{title: 1, year: 1},
]

// callback
collection.findOne( ...query, (e, docs) => { /* .. */ });

// promise
collection
  .findOne(...query)
  .then(doc => {
    const title = doc.title;
    // do something..
   })
   .catch(e => {
    console.log('error: ' + e);
  });


// async
const match = await collection.findOne(...query);
console.log(match.title);

// or directly access the title
const {title} = await collection.findOne(...query);
```

<br><br>

#### find object id
```javascript
// method #1
var ObjectId = require('mongodb').ObjectId;
var id = "5f2a40a54d054559dcc566ff";
var o_id = new ObjectId(id);
const query = {"itemdetails._id":o_id};

// callback
collection.findOne(query, (e, docs) => { /* .. */ });

// async
const r = await collection.findOne(query)




// method #2
const r = await collection.insertOne(obj);

// you can access the id of the result by using "insertedId)"
const query = {_id: ObjectId(r.insertedId)};

// callback
collection.findOne(query, (e, r) => { /* .. */ });

// async
const r = await collection.findOne(query)
```

<br><br>


## Check if field exist ($exists)
```javascript
const query = {"payload.discount": {$exists: true}};

// callback.insertOne
collection.findOne(query, (e, docs) => { /* .. */ });

// async
// example #1
const r = await collection.findOne(query)
```















<br><br>


## .find


#### get all documents from collection
```javascript
// async
const query = {};

// callback
collection.find(query).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.find(query).toArray({});
```

<br><br>


#### go to next result (cursor)
```javascript
// async
const result = await collection.find({title: 'any movie'});
let {title} = await result.next();
let {title2} = await result.next();
```

<br><br>


#### filter result ascending order (cursor) - .sort
- https://docs.mongodb.com/manual/reference/method/cursor.sort/
```javascript
const query = [
{title: "any title"},
{projection: {title: 1, year: 1}},
]

// sync
const result = collection.find(query).sort([["year", 1]]);
```

#### skip results (cursor)
- https://docs.mongodb.com/manual/reference/method/cursor.skip/
```javascript
const query = [
{title: "any title"},
{projection: {title: 1, year: 1}},
]

// sync - skip 5 results
const result = collection.find(query).sort([["year", 1]]).skip(5);
```

<br><br>

#### create pagination (cursor)
- https://docs.mongodb.com/manual/reference/method/cursor.skip/
```javascript
// sync - Page is increasing every iteration ++ - We always show 20 items each page
const moviesPerPage = 20;
const skipMovies = page>0 ? page*moviesPerPage : 0;
const displayCursor = collection.find(query).limit(moviesPerPage).skip(skipMovies);
```



<br><br>
<br><br>


#### query array
```javascript
const countries = ['nyc', 'paris'];
const query = {countries: { $in: countries }};

// callback
collection.find(query).toArray(function(e, docs) { /* .. */ });

// async
const result = await collection.find(query).toArray({});
```
<br><br>

#### find specific data and expect multiple results
```javascript
// callback
collection.find( {"token": token} ).toArray(function(e, docs) { /* .. */ });

// async
const verify = await collection.find({"token": token}).toArray({});
```

<br><br>

#### find multiple documents that match query
```javascript
const query = {title: {$all: ['sci-fi', 'action']}};

// callback
collection.find(query).toArray(function(e, docs) { /* .. */ });

// async
const verify = await collection.find(query).toArray({});
```

<br><br>



#### find next alphabetic document with used = 0 and limit to 2 item
```javascript
// callback
collection.find( {"used": 0} ).limit( 2 ).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.find( {"used": 0} ).limit( 2 ).toArray({});
```

<br><br>

#### find value in same document with multiple possible matches for the same field (https://docs.mongodb.com/manual/reference/operator/query/in/)
```javascript
// callback
collection.find( {title: {$in: ['some title', 'some other title']}} ).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.find( {title: {$in: ['some title', 'some other title']}} ).toArray({});
```

<br><br>

#### find multiple values in same document, only if all search values can be found (https://docs.mongodb.com/manual/reference/operator/query/and/#op._S_and)
```javascript
// callback
collection.find( { $and: [{"client_id": json?.client_id}, {"client_secret": json?.client_secret}] } ).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.find( { $and: [{"client_id": json?.client_id}, {"client_secret": json?.client_secret}] } ).toArray({});
```

<br><br>

#### find multiple values in same document, only if atleast one search value can be found (https://docs.mongodb.com/manual/reference/operator/query/or/#op._S_or)
```javascript
// callback
collection.find( { $or: [{"client_id": json?.client_id}, {"client_secret": json?.client_secret}] } ).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.find( { $or: [{"client_id": json?.client_id}, {"client_secret": json?.client_secret}] } ).toArray({});
```












<br><br><br><br>


#### Using temp files on disk at large searches (https://docs.mongodb.com/manual/reference/method/cursor.allowDiskUse/)
```javascript
const query = {"payload.discount": {$exists: true}};

// await
const r = await collection.findOne(query).allowDiskUse();
```





































<br><br>

____________________________________________________
____________________________________________________

<br><br>



# Aggregation - .aggregate (https://docs.mongodb.com/manual/reference/aggregation/)
- Aggregation is a pipleline
- Pipelines are composed of one or more stages
- Stages use one or more expressions
- Expressions are functions
```javascript
const pipeline = [
  [{stage1}, {stage2}, {stage3}],
  {options}
];

// callback
collection.aggregate(...pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(...pipeline).toArray({});
```

## Ref
- https://docs.mongodb.com/manual/reference/command/aggregate/


## Guides
- What can I understand under aggregation? (https://www.youtube.com/watch?v=5_oSSbQpGSM)
- Structure and Syntax (https://www.youtube.com/watch?v=SYtRQ5crN6U)
- m220 Basic Aggregation (https://www.youtube.com/watch?v=dpr_2cbC4Yk)







<br><br>
<br><br>

## Expressions (https://youtu.be/SYtRQ5crN6U?t=172)
- https://docs.mongodb.com/manual/reference/aggregation-variables/
```javascript
// Field Path - Access the field inside of a document
'$fieldName'       ('$apples')

// System Variable - Will be always with uppercase and is on system level. $$CURRENT reference to the current document.
'$$UPPERCASE'       ('$$CURRENT')

// User Variable - Will be as example used by let inside of lookup
'$$foo'
```
















<br><br>
<br><br>

## Operator

<br><br>

#### use operator inside of another one
```javascript
/* our collection looks like this:
{ "_id" : 1, "item" : "abc", "price" : 10, "discount": 2, taxes: 2, date: ISODate("2014-03-01T08:00:00Z") }
{ "_id" : 2, "item" : "jkl", "price" : 20, "discount": 2, taxes: 2, date: ISODate("2014-03-01T09:00:00Z") }
{ "_id" : 3, "item" : "xyz", "price" : 5, "discount": 2, taxes: 2, date: ISODate("2014-03-15T09:00:00Z") }
*/

const pipeline = [
  {$project: {date: 1, item: 1, newPrice: {$divide: [{$add: ["$price", "$taxes"]}, "$discount"]}}}
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
The operation returns the following results:
{ "_id" : 1, "item" : "abc", "date" : ISODate("2014-03-01T08:00:00Z"), "newPrice" : 6 }
{ "_id" : 2, "item" : "jkl", "date" : ISODate("2014-03-01T09:00:00Z"), "newPrice" : 11 }
{ "_id" : 3, "item" : "xyz", "date" : ISODate("2014-03-15T09:00:00Z"), "newPrice" : 3.5 }
*/
```


<br><br>

#### $project (https://docs.mongodb.com/manual/reference/operator/aggregation/project/)
- The logic is same to **projection** but **$project** got way more options.

<br><br>

#### create new field based of value
```javascript
/*
{
  '_id': '12345678',
  'used': 0,
  'title': 'Fortnite',
  'date': [
     'year': 2015
   ]
}
*/

const pipeline = [
  {$match: {used: 0}},
  {$project: {title: 1, _id: 0, year: '$date.year'}},
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
{
  'title': 'Fortnite',
  'year': 2015,
}
*/
```

















<br><br>


## $group (https://docs.mongodb.com/manual/reference/operator/aggregation/group/)

<br><br>


#### count amount of field with the same value
- In this case we also sort the result descending and then limit the result to 20
```javascript
/* // One of documents looks like this:
{
    "_id": {
        "$oid": "5a9427648b0beebeb69579cc"
    },
    "name": "Andrea Le",
    "email": "andrea_le@fakegmail.com",
    "movie_id": {
        "$oid": "573a1390f29313caabcd418c"
    },
    "text": "Rem officiis eaque repellendus amet eos doloribus. Porro dolor voluptatum voluptates neque culpa molestias. Voluptate unde nulla temporibus ullam.",
    "date": {
        "$date": "2012-03-26T23:20:16.000Z"
    }
}
*/


const pipeline = [
        {
          '$group': {
            '_id': '$email',
            'count': {
              '$sum': 1
            }
          }
        }, {
          '$sort': {
            'count': -1
          }
        }, {
          '$limit': 20
        }
      ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
_id:"roger_ashton-griffiths@gameofthron.es"
count:331

_id:"nathalie_emmanuel@gameofthron.es"
count:327
*/
```



<br><br>
<br><br>


## get number between range
```javascript
// match results with year between 1980-1990
const pipeline = [{$match: {year: {'$gte': 1980, '$lt': 1990}}}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});
```


<br><br>


## matchdom document with used = 0 and limit to 1 item
```javascript
// method #1
const pipeline = [{$match: { used: 0 }}, {$limit: 1}];

// method #2
const pipeline = [{$match: { used: 0 }}, {$sample: { size: 1 }}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});
```
<br><br>

## match random document with used = 0 and limit to 1 item and return only title and _id
```javascript
const pipeline = [
{$match: { used: 0 }},
{$project: { title: 1, _id: 1 }},
{$limit: 1},
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});
```

<br><br>

## sort ascending order (https://docs.mongodb.com/manual/reference/operator/aggregation/sort/)
```javascript
// sort results by year
const pipeline = [{ $sort: {year: 1}}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});
```

<br><br>

## skip results (https://docs.mongodb.com/manual/reference/operator/aggregation/skip/)
```javascript
// sort results by year
const pipeline = [{$skip: 5}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});
```






<br><br>


#### Using temp files on disk at large searches
```javascript
// sort results by year
const pipeline = [
  [{ $sort: {year: 1}}],
  {allowDiskUse: true}
];

// callback
collection.aggregate(...pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(...pipeline).toArray({});
```
























<br><br>
<br><br>

## Join

<br><br>


#### $lookup (https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/)
- Allows us to apply aggregation pipelines before the data is joined

<br><br>


- **from** (Specifies the collection in the same database to perform the join with. The from collection cannot be sharded.) - https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/#lookup-join-from

<br>

- **let** (Specifies variables to use in the pipeline field stages. Use the variable expressions to access the fields from the documents input to the $lookup stage.
- In other words the pipleline only has access to the current collection where we run the lookup. To get access from the source collection where we run the join we use let to define the fields where we want access) - https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/#lookup-join-let

<br>

- **pipeline** (Specifies the pipeline to run on the joined collection. The pipeline determines the resulting documents from the joined collection. To return all documents, specify an empty pipeline [].) - https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/#lookup-join-pipeline

<br>

- **as** (Specifies the name of the new array field to add to the input documents. The new array field contains the matching documents from the from collection. If the specified name already exists in the input document, the existing field is overwritten.) - https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/#lookup-join-as


```javascript
const pipeline = [
  {
    '$match': {
      'year': {
        '$gte': 1980, 
        '$lt': 1990
      }
    }
  }, {
    '$lookup': {
      'from': 'comments', 
      'let': {
        'id': '$_id'
      }, 
      'pipeline': [
        {
          '$match': {
            '$expr': {
              '$eq': [
                '$movie_id', '$$id'
              ]
            }
          }
        }
      ], 
      'as': 'movie_comments'
    }
  }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});
```


<br><br>


#### guides
- https://www.youtube.com/watch?v=j7ccC2F1yc0

<br><br><br><br>


#### show the amount of matches - $count (https://docs.mongodb.com/manual/reference/operator/aggregation/count/)
- Because we use a pipeline we will first match all the movie comments and then after this only response with the amount of matches as result
```javascript
const pipeline = [
  {
    '$match': {
      'year': {
        '$gte': 1980, 
        '$lt': 1990
      }
    }
  }, {
    '$lookup': {
      'from': 'comments', 
      'let': {
        'id': '$_id'
      }, 
      'pipeline': [
        {
          '$match': {
            '$expr': {
              '$eq': [
                '$movie_id', '$$id'
              ]
            }
          }
        }, {
          '$count': 'count'
        }
      ], 
      'as': 'movie_comments'
    }
  }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});
```








<br><br>


#### sort lookup results
- In this example we want to sort the comments we lookup by date. Inside of the lookup pipeline we can use **{ '$sort': { 'date': -1 }** and access date. All fields from the document we want to lookup are avaible in our pipeline. If we want to access fields from the source document we would have to use **let** like in this example with the movie ID.
- 
```javascript
/* // comments document
{
    "_id": {
        "$oid": "5a9427648b0beebeb69579cc"
    },
    "name": "Andrea Le",
    "email": "andrea_le@fakegmail.com",
    "movie_id": {
        "$oid": "573a1390f29313caabcd418c"
    },
    "text": "Rem officiis eaque repellendus amet eos doloribus. Porro dolor voluptatum voluptates neque culpa molestias. Voluptate unde nulla temporibus ullam.",
    "date": {
        "$date": "2012-03-26T23:20:16.000Z"
    }
}
*/

/* // source document
{
    "_id": {
        "$oid": "573a1390f29313caabcd4135"
    },
    "plot": "Three men hammer on an anvil and pass a bottle of beer around.",
    "genres": ["Short"],
    "runtime": 1,
    "cast": ["Charles Kayser", "John Ott"],
    "num_mflix_comments": 1,
    "title": "Blacksmith Scene",
    "fullplot": "A stationary camera looks at a large anvil with a blacksmith behind it and one on either side. The smith in the middle draws a heated metal rod from the fire, places it on the anvil, and all three begin a rhythmic hammering. After several blows, the metal goes back in the fire. One smith pulls out a bottle of beer, and they each take a swig. Then, out comes the glowing metal and the hammering resumes.",
    "countries": ["USA"],
    "released": {
        "$date": "1893-05-09T00:00:00.000Z"
    },
    "directors": ["William K.L. Dickson"],
    "rated": "UNRATED",
    "awards": {
        "wins": 1,
        "nominations": 0,
        "text": "1 win."
    },
    "lastupdated": "2015-08-26 00:03:50.133000000",
    "year": 1893,
    "imdb": {
        "rating": 6.2,
        "votes": 1189,
        "id": 5
    },
    "type": "movie",
    "tomatoes": {
        "viewer": {
            "rating": 3,
            "numReviews": 184,
            "meter": 32
        },
        "lastUpdated": {
            "$date": "2015-06-28T18:34:09.000Z"
        }
    }
}
*/



const pipeline = [
  {
    '$match': {
      '_id': new ObjectId('573a13b5f29313caabd42c2f')
    }
  }, {
    '$lookup': {
      'from': 'comments', 
      'let': {
        'id': '$_id'
      }, 
      'pipeline': [
        {
          '$match': {
            '$expr': {
              '$eq': [
                '$movie_id', '$$id'
              ]
            }
          }
        }, {
          '$sort': {
            'date': -1
          }
        }
      ], 
      'as': 'comments'
    }
  }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});
```






































































<br><br>

____________________________________________________
____________________________________________________

<br><br>


# Insert/Write Data

<br><br>

## add timestamp to insert
```javascript
// MongoDB will automatically conert new Date() to 2020-09-14T17:04:55.281+00:00
// also nice to know your object id already includes a timestamp too..
{"created_at": new Date()}
```

<br><br>

## write concern (https://docs.mongodb.com/manual/reference/write-concern/)
- Not defined write concern will be always "1". This means the data will be only written to 1 primary node (database)

<br><br>
- If set to "0" it means it does not request a result of the write process. "Fire-and-forget". This is usefully when you want the fastest possible write process and do not care if some data gets lost. As example for real time monoitoring operations.

<br><br>
- In a 3-node replica set, the highest valid Write Concern is 3. A Write Concern of w: 5 or w: 4 would never be satisfied, because there are only 3 nodes in the set.

<br><br>
- If set to "majority" it will wait until the data gets replicated to a secondary node. The secondary node send the result back to the primary and the primary back to the client. (https://docs.mongodb.com/manual/reference/write-concern/#writeconcern.%22majority%22)
- If set to "majority" you should **always** use a write concern timeout **{w: 'majority', wtimeout: 5000}**
```javascript
const ar = [
{"title": "Fortnite", "year": 2015}, // document to add to collection
{w: 'majority', wtimeout: 5000} // options
];

// callback
collection.insertOne(...ar, function(e, r) { /* .. */ });

//async
const r = await collection.insertOne(...ar);
```

#### Guides
- https://www.youtube.com/watch?v=RIeSCrq6PHg


<br><br>


## .insertOne (https://docs.mongodb.com/manual/reference/method/db.collection.insertOne/)
- Insert only 1 document
- Below example explains the insertOneWriteOpResult (https://www.youtube.com/watch?v=UzLB7a2YOOM)
```javascript
const obj = {"title": "Fortnite", "year": 2015};

// callback
collection.insertOne(obj, function(e, r) { /* .. */ });

//async
const r = await collection.insertOne(obj);

// When we insert a document we get an insertOneWriteOpResult back
// n is the total documents inserted
// ok means database responded that the command executed correctly
let {n, ok} = r.result;

// alternative you can check the amount of inserted documents by using "insertedCount"
console.log(r.insertedCount); // 1

// get the id from the document
console.log(r.insertedId);

// So in case of our example n will be 1 cause we inserted 1 document
// And ok will be 1 too is the insert process worked as exapected
console.log(n); // 1
console.log(ok); // 1
```







<br><br><br><br>


## .insertMany (https://docs.mongodb.com/manual/reference/method/db.collection.insertMany/)
- Insert multiple documents
- Below example explains the insertOneWriteOpResult: (https://youtu.be/UzLB7a2YOOM?t=178)
```javascript
const ar = [
  {title: 'Fortnite', year: 2015},
  {title: 'Fifa', year: 2016},
  {title: 'Halo', year: 2017},
];

// callback
collection.insertMany(ar, function(e, r) { /* .. */ });

//async
const r = await collection.insertMany(ar);

// Just like .insertOne we get a result object back
// n is the total documents inserted
// ok means database responded that the command executed correctly
let {n, ok} = r.result;

// alternative you can check the amount of inserted documents by using "insertedCount"
console.log(r.insertedCount); // 1

// returns array with the ids from the documents
console.log(r.insertedIds);

// So in case of our example n will be 1 cause we inserted 1 document
// And ok will be 1 too is the insert process worked as exapected
console.log(n); // 1
console.log(ok); // 1
```








































## Update


#### .updateOne (https://docs.mongodb.com/manual/reference/method/db.collection.updateOne/)
- Update single document
- If multiple matches are found then only the first match will be updated
- Below example explain the result object that comes back: (https://youtu.be/UzLB7a2YOOM?t=235)
```javascript
const ar = [
  // search query
  {url: urlhere},
  
  // fields to update
  {$set: { used: 1 }},
  
  // options paramater
  // if query doesnt find a document, it will create a new document
  {upsert: true},
];

// callback
collection.updateOne(...ar, function(e, res) {/* .. */ });

// async
const r = await collection.updateOne(...ar);

// get amount of documents that have been modified
console.log(r.result.nModified);

// get result of upserted
console.log(r.result.upserted);

// get amount of matched documents (search query object)
console.log(r.matchedCount);

// get amount of modified/updated documents
console.log(r.modifiedCount);

// get id of new document if upserted was successfully
console.log(r.upsertedId);
```


<br><br>


#### update document and increase/decrease specific field (https://docs.mongodb.com/manual/reference/operator/update/inc/)
```javascript
/*
{ Original Document:
  _id: 1,
  sku: "abc123",
  quantity: 10,
  metrics: {
    orders: 2,
    ratings: 3.5
  }
}
*/

const ar = [
  // search query
  { sku: "abc123" },
  
  // decrease quantity and increase orders
  {$inc: {quantity: -2, "metrics.orders": 1}},
];

// callback
collection.updateOne(...ar, function(e, res) {/* .. */ });

// async
const r = await collection.updateOne(...ar);

/*Result:
{
   "_id" : 1,
   "sku" : "abc123",
   "quantity" : 8,
   "metrics" : {
      "orders" : 3,
      "ratings" : 3.5
   }
}
*/
```






<br><br><br><br>








#### .updateMany (https://docs.mongodb.com/manual/reference/method/db.collection.updateMany/)
- Update multiple documents
- https://youtu.be/xq2_ht-cZHc?t=89
```javascript
const ar = [
  // search query
  {url: urlhere},
  
  // fields to update
  {$set: { used: 1 }},
  
  // options paramater
  // if query doesnt find a document, it will create a new document
  {upsert: true},
];

// callback
collection.updateOne(...ar, function(e, res) {/* .. */ });

// async
const r = await collection.updateOne(...ar);

// get amount of matched documents (search query object)
console.log(r.matchedCount);

// get amount of modified/updated documents
console.log(r.modifiedCount);
```















































<br><br><br><br>



## .bulkWrite (https://docs.mongodb.com/manual/reference/method/db.collection.bulkWrite/)
- Performs multiple write operations with controls for order of execution.
- Execution will be in order they got applied.
- If any operation is not executed successfully the **next operation and all operations after this will be canceld!** But all operations before the error were written.


```javascript
const ar = [
   {insertOne: {title: 'Fortnite'}},
   {insertOne: {title: 'COD'}},
];

// callback
collection.bulkWrite(...ar, function(e, res) {/* .. */ });

// async
const r = await bulkWrite(...ar;





// example for update
const ar = [
  // search query
  {url: urlhere},
  
  // fields to update
  {$set: { used: 1 }},
];

// callback
collection.bulkWrite(...ar, function(e, res) {/* .. */ });

// async
const r = await collection.bulkWrite(...ar);
```


<br><br><br><br>



#### parallel/async (non blocking) execution
- Does not stop if any execution fails but the results will show us later if any fails.
```javascript
const ar = [
  [
    {insertOne: {title: 'Fortnite'}},
    {insertOne: {title: 'COD'}},
  ],
  {ordered: false},
];

// callback
collection.bulkWrite(...ar, function(e, res) {/* .. */ });

// async
const r = await collection.bulkWrite(...ar);
```











































<br><br>

____________________________________________________
____________________________________________________

<br><br>


# Delete

## What actually happens when we delete a document?
- Collection data will be changed
- Indexes will be updated
- Entries in the oplog will be added (oplog is the mechanism that allows to replicate data)


<br><br>




## .deleteOne (https://docs.mongodb.com/manual/reference/method/db.collection.deleteOne/)
- **IMPORTANT** - When using .deleteOne make sure that your match query will 100% match the document you want to delete or your may delete the wrong one. As example try always to use document IDs for the match query.
```javascript
const query = {id: anyID};

// callback
collection.deleteOne(query, function(e, result) { /* .. */ });

//async
const r = await collection.deleteOne(query);

// check if delete was successfully
console.log(r.result.n); // should be 1 if successfully and 0 if not
```

<br><br>



## delete single document without match query
- It will choose the first document that can be found in natural order.
```javascript
const query = {};

// callback
collection.deleteOne(query, function(e, result) { /* .. */ });

//async
const r = await collection.deleteOne(query);
```








<br><br><br><br>


## .deleteMany (https://docs.mongodb.com/manual/reference/method/db.collection.deleteMany/)
- delete multiple documents
```javascript
const query = {url: yoururl};

// callback
collection.deleteOne(query, function(e, result) { /* .. */ });

//async
const r = await collection.deleteOne(query);

// check if delete was successfully
console.log(r.result.n); // gives the amount of deleted documents. If 4 documents was deleted then we get here 4. If 0 documents was deleted then we get 0.
```





























































































<br><br>

____________________________________________________
____________________________________________________

<br><br>


# Error Handling

<br><br>

## Duplicated Key Error (E11000 duplicate key error collection)
- https://youtu.be/ELazfOluptY?t=24
```javascript
const query = {_id: 0};

// callback
collection.insertOne(query, function(e, result) {
  if(e){
    console.log(e.errmsg); // E11000 duplicate key error collection
    throw new Error(e);
  }
});

//async
const r = await collection.insertOne(query);

// try to insert a new document with same  ID
try{
  const r = await collection.insertOne(query);
} catch (e) {
  console.log(e.errmsg); // E11000 duplicate key error collection
}
```

<br><br>

## Timeout Error
- https://youtu.be/ELazfOluptY?t=81
- In order to prevent app crashes add a timeout by using write timeout **{wtimeoutMS: 2000}** and add a try/catch block to prevent crashes and to catch the error.
- You can avoid problems by lower the write concern value or by increasing the write concern timeout.
```javascript
const ar = [
  {_id: 0},
  {wtimeoutMS: 2000},
];

try{
  const r = await collection.insertOne(...ar);
} catch (e) {
  console.log(e);
}
```


<br><br>

## writeConcernError
- https://youtu.be/ELazfOluptY?t=122
- In this example we told our insert operation that we have 5 nodes {w: 5} but our cluster actually only got 3. We will get back a writeConcernError which gives us more details (https://youtu.be/ELazfOluptY?t=146) 
```javascript
const ar = [
  {_id: 0},
  {w: 5},
];

try{
  const r = await collection.insertOne(...ar);
} catch (e) {
  console.log(e.result.writeConcernError);
}
```






