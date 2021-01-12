# MongoDB Cheat Sheet
MongoDB Cheat Sheet with the most needed stuff..


# Guides
- MongoDB Course (https://university.mongodb.com/courses/M220JS/about)












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
____________________________________________________
____________________________________________________
<br><br>


# Community Server
- https://www.mongodb.com/try/download/community
- Ubuntu 20.04 - amd64 (https://repo.mongodb.org/apt/ubuntu/dists/focal/mongodb-org/4.4/multiverse/binary-amd64/mongodb-org-server_4.4.2_amd64.deb)

<br><br>
## MAC
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

## Fedora:
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

## CentOS:
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

## Ubuntu:
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

## Windows:
- MongoDB Server should get an autostart entry by default after installation.
Start Command:
```bash
net start MongoDB
```
Stop Command:
```bash
net stop MongoDB
```























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


# srv (service record)
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

# localhost url
- mongodb://localhost:27017



























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

# Logical Query Operators

## Comparison Query Operators (https://docs.mongodb.com/manual/reference/operator/query-comparison/)
- $eq	Matches values that are equal to a specified value.
- $gt	Matches values that are greater than a specified value.
- $gte	Matches values that are greater than or equal to a specified value.
- $in	Matches any of the values specified in an array.
- $lt	Matches values that are less than a specified value.
- $lte	Matches values that are less than or equal to a specified value.
- $ne	Matches all values that are not equal to a specified value.
- $nin	Matches none of the values specified in an array.

<br><br>

## Logical Query Operators (https://docs.mongodb.com/manual/reference/operator/query-logical/)
- $and	Joins query clauses with a logical AND returns all documents that match the conditions of both clauses.
- $not	Inverts the effect of a query expression and returns documents that do not match the query expression.
- $nor	Joins query clauses with a logical NOR returns all documents that fail to match both clauses.
- $or	Joins query clauses with a logical OR returns all documents that match the conditions of either clause.

<br><br>

## Element Query Operators (https://docs.mongodb.com/manual/reference/operator/query-element/)
- $exists	Matches documents that have the specified field.
- $type	Selects documents if a field is of the specified type.

<br><br>

## Element Query Operators (https://docs.mongodb.com/manual/reference/operator/query-evaluation/)
- $expr	Allows use of aggregation expressions within the query language.
- $jsonSchema	Validate documents against the given JSON Schema.
- $mod	Performs a modulo operation on the value of a field and selects documents with a specified result.
- $regex	Selects documents where values match a specified regular expression.
- $text	Performs text search.
- $where	Matches documents that satisfy a JavaScript expression.

<br><br>

## Geospatial Query Operators (https://docs.mongodb.com/manual/reference/operator/query-geospatial/)
- $geoIntersects	Selects geometries that intersect with a GeoJSON geometry. The 2dsphere index supports $geoIntersects.
- $geoWithin	Selects geometries within a bounding GeoJSON geometry. The 2dsphere and 2d indexes support $geoWithin.
- $near	Returns geospatial objects in proximity to a point. Requires a geospatial index. The 2dsphere and 2d indexes support $near.
- $nearSphere	Returns geospatial objects in proximity to a point on a sphere. Requires a geospatial index. The 2dsphere and 2d indexes support $nearSphere.


<br><br>

## Array Query Operators (https://docs.mongodb.com/manual/reference/operator/query-array/)
- $all	Matches arrays that contain all elements specified in the query.
- $elemMatch	Selects documents if element in the array field matches all the specified $elemMatch conditions.
- $size	Selects documents if the array field is a specified size.


<br><br>

## Bitwise Query Operators (https://docs.mongodb.com/manual/reference/operator/query-bitwise/)
- $bitsAllClear	Matches numeric or binary values in which a set of bit positions all have a value of 0.
- $bitsAllSet	Matches numeric or binary values in which a set of bit positions all have a value of 1.
- $bitsAnyClear	Matches numeric or binary values in which any bit from a set of bit positions has a value of 0.
- $bitsAnySet	Matches numeric or binary values in which any bit from a set of bit positions has a value of 1.




















<br><br>

____________________________________________________
____________________________________________________

<br><br>



## MongoDB bin locations
```bash
#windows
"C:\Program Files\MongoDB\Server\4.2\bin"
```










<br><br>

____________________________________________________
____________________________________________________

<br><br>

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


<br><br>

____________________________________________________
____________________________________________________

<br><br>




# Async

## Result
```javascript

const query = { id: json.id };
const newValue = { $set: { title: json.title } };

const r = await collection.updateOne(query, newValue);
console.log( 'updatePizza() - result:' + JSON.stringify(r, null, 4) );

/*
// if not successfully you will get r.result.n == 0
r: {"result":{"n":0,"nModified":0,"ok":1},"connection":{"_events":{},"_eventsCount":4,"id":1,"address":"127.0.0.1:27017","bson":{},"socketTimeout":360000,"host":"localhost","port":27017,"monitorCommands":false,"closed":false,"destroyed":false,"lastIsMasterMS":5},"modifiedCount":0,"upsertedId":null,"upsertedCount":0,"matchedCount":0,"n":0,"nModified":0,"ok":1}

// if successfully you will get r.result.n == 1
r: {"result":{"n":1,"nModified":1,"ok":1},"connection":{"_events":{},"_eventsCount":4,"id":1,"address":"127.0.0.1:27017","bson":{},"socketTimeout":360000,"host":"localhost","port":27017,"monitorCommands":false,"closed":false,"destroyed":false,"lastIsMasterMS":1},"modifiedCount":1,"upsertedId":null,"upsertedCount":0,"matchedCount":1,"n":1,"nModified":1,"ok":1}
*/
```

<br><br>

____________________________________________________
____________________________________________________

<br><br>

# Connect

```javascript
let myDB;
const options = {
  useNewUrlParser: true,
  useUnifiedTopology: true,
  connectTimeoutMS: 200,
  retryWrites: true,
}

// callback
MongoClient.connect(MongoDB_DB_URL, options, function(e, client) {

   if(e) throw new Error('Error while try to connect to MongoDB Database - error: ' + e);

   console.log( 'MongoDB - Connected successfully to server..' );
   myDB = client.db( MongoDB_DB_NAME );

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
        return {code : "SUCCESS"};
      } catch (e) {
        log( chalk.red.bold('❌ ERROR') + ' Error while try to connect to MongoDB Database - ' + chalk.white.bold('error:\n') + e );
        return {code : "ERROR", e: e};
      }

};
```








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


# countDocuments
- count all documents from collection
```javascript
const myDB = client.db(MongoDB_DB_NAME);
const movies = myDB.collection('movies');
const numMovies = await movies.countDocuments({}); // <-- will be number of documents
```



































<br><br>

____________________________________________________
____________________________________________________

<br><br>


# Find Data


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
<br><br>

____________________________________________________
____________________________________________________

<br><br>



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
var ObjectId = require('mongodb').ObjectId;
var id = "5f2a40a54d054559dcc566ff";
var o_id = new ObjectId(id);

// callback
collection.findOne( {"itemdetails._id":o_id}, (e, docs) => { /* .. */ });

// async
const r = await collection.findOne( {"itemdetails._id":o_id} )
```

<br><br>


## Check if field exist ($exists)
```javascript
const query = {"payload.discount": {$exists: true}};

// callback
collection.findOne(query, (e, docs) => { /* .. */ });

// async
// example #1
const r = await collection.findOne(query)
```















<br><br>


## .find


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

<br />

#### find value in same document with multiple possible matches for the same field (https://docs.mongodb.com/manual/reference/operator/query/in/)
```javascript
// callback
collection.find( {title: {$in: ['some title', 'some other title']}} ).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.find( {title: {$in: ['some title', 'some other title']}} ).toArray({});
```

<br />

#### find multiple values in same document, only if all search values can be found (https://docs.mongodb.com/manual/reference/operator/query/and/#op._S_and)
```javascript
// callback
collection.find( { $and: [{"client_id": json?.client_id}, {"client_secret": json?.client_secret}] } ).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.find( { $and: [{"client_id": json?.client_id}, {"client_secret": json?.client_secret}] } ).toArray({});
```

#### find multiple values in same document, only if atleast one search value can be found (https://docs.mongodb.com/manual/reference/operator/query/or/#op._S_or)
```javascript
// callback
collection.find( { $or: [{"client_id": json?.client_id}, {"client_secret": json?.client_secret}] } ).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.find( { $or: [{"client_id": json?.client_id}, {"client_secret": json?.client_secret}] } ).toArray({});
```





































<br><br>

____________________________________________________
____________________________________________________

<br><br>



# aggregation (.aggregate)


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

## matchdom document with used = 0 and limit to 1 item
```javascript
// method #1
const query = [{$match: { used: 0 }}, {$limit: 1}];

// method #2
const query = [{$match: { used: 0 }}, {$sample: { size: 1 }}];

// callback
collection.aggregate(query).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(query).toArray({});
```
<br><br>

## match random document with used = 0 and limit to 1 item and return only title and _id
```javascript
const query = [
{$match: { used: 0 }},
{$project: { title: 1, _id: 1 }},
{$limit: 1},
];

// callback
collection.aggregate(query).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(query).toArray({});
```

<br><br>

## sort ascending order (https://docs.mongodb.com/manual/reference/operator/aggregation/sort/)
```javascript
// sort results by year
const query = [{ $sort: {year: 1}}];

// callback
collection.aggregate(query).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(query).toArray({});
```

<br><br>

## skip results (https://docs.mongodb.com/manual/reference/operator/aggregation/skip/)
```javascript
// sort results by year
const query = [{$skip: 5}];

// callback
collection.aggregate(query).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(query).toArray({});
```

<br><br>


## $add (https://docs.mongodb.com/manual/reference/operator/aggregation/add/)

#### add numbers
```javascript
// add price + fee
const query = [{$project: {item: 1, total: {$add: [ "$price", "$fee" ]}}}];

// callback
collection.aggregate(query).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(query).toArray({});
```

<br><br>


## $group (https://docs.mongodb.com/manual/reference/operator/aggregation/group/)

#### find average of number - $avg
- https://docs.mongodb.com/manual/reference/operator/aggregation/avg/#grp._S_avg
```javascript
/* Our collection looks like this:
{ "_id" : 1, "item" : "abc", "price" : 10, "quantity" : 2, "date" : ISODate("2014-01-01T08:00:00Z") }
{ "_id" : 2, "item" : "jkl", "price" : 20, "quantity" : 1, "date" : ISODate("2014-02-03T09:00:00Z") }
{ "_id" : 3, "item" : "xyz", "price" : 5, "quantity" : 5, "date" : ISODate("2014-02-03T09:05:00Z") }
{ "_id" : 4, "item" : "abc", "price" : 10, "quantity" : 10, "date" : ISODate("2014-02-15T08:00:00Z") }
{ "_id" : 5, "item" : "xyz", "price" : 5, "quantity" : 10, "date" : ISODate("2014-02-15T09:12:00Z") }
*/


const query = [{$group: {
                 _id: "$item",
                avgAmount: { $avg: { $multiply: [ "$price", "$quantity" ] } },
                avgQuantity: { $avg: "$quantity" }
              }}];

// callback
collection.aggregate(query).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(query).toArray({});

/* operation will return:
{ "_id" : "xyz", "avgAmount" : 37.5, "avgQuantity" : 7.5 }
{ "_id" : "jkl", "avgAmount" : 20, "avgQuantity" : 1 }
{ "_id" : "abc", "avgAmount" : 60, "avgQuantity" : 6 }
*/
```























<br><br>
____________________________________________________
____________________________________________________

<br><br>


# Update


## Update specific field
```javascript

var query = { url: t33n.url };
var newvalues = { $set: { used: 1 } };

// callback
collection.updateOne(query, newvalues, function(e, res) { /* .. */ });

// async
const r = await collection.updateOne(query, newvalues);
```



<br><br>

____________________________________________________
____________________________________________________

<br><br>


# Insert


## Insert single object
```javascript
// callback
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





<br><br>

____________________________________________________
____________________________________________________

<br><br>


# Delete


## Delete specific data
```javascript
// callback
collection.deleteOne({"id": json.id}, function(e, result) { /* .. */ });

//async
const r = await collection.deleteOne( {"id": json.id} );
```




