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
<br>

Start Command:
```bash
sudo service mongod start
```
<br>

Stop Command:
```bash
sudo service mongod stop
```
<br>

Enable in general:
```bash
sudo systemctl enable mongod
```

<br>

Alternative Install Method:
```bash
sudo dnf update

cat <<EOF | sudo tee /etc/yum.repos.d/mongodb.repo
[mongodb-4.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/7/mongodb-org/4.2/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-4.2.asc
EOF

sudo dnf -y install mongodb-org

mongo -version
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

# CLI (https://docs.mongodb.com/manual/mongo/)

<br><br>

## MongoDB bin locations
```bash
#windows
"C:\Program Files\MongoDB\Server\4.2\bin"
```




<br><br>

## create user
```bash
use admin
db.createUser({ user: "sa" , pwd: "sample", roles: ["userAdminAnyDatabase", "dbAdminAnyDatabase", "readWriteAnyDatabase"]})
```



<br><br>

## delete user
```bash
db.dropUser('usernamehere')
```



<br><br>
<br><br>



## Mongoexport
- Export Database/Collections to .json

<br><br>

#### Export specific collection with ALL fields to .json
```bash
# --jsonArray will generated one json file. If not activated solo objects will be created to each document
# --pretty will pretty print the JSON to be human read able
# https://docs.mongodb.com/manual/reference/program/mongoexport
mongoexport --jsonArray --pretty -h id.mongolab.com:60599 -u username -p password -d mydb -c mycollection -o mybackup.json
```











<br><br><br><br>



## bsondump (https://docs.mongodb.com/database-tools/bsondump/#mongodb-binary-bin.bsondump)
- Convert BSON to JSON

<br><br>

#### dump entire database to BSON files
```bash
bsondump --pretty --db db1
```

<br><br>

#### convert all BSON files recursive from folder to JSON
```bash
#!/bin/sh
cd "$(dirname "$0")"
printf "\nWe will display now the current directory used:"; pwd

RegexMatchS3="https:[/][/]s3-eu-central-1[.]amazonaws[.]com[/][^'\"\`\]\\\]+"
RegexMatchS3Host="https:[/][/]s3-eu-central-1[.]amazonaws[.]com[/]"

NewHost="https://anygooglelinkhere.com/"

MongoDBURI="mongodb://user:pw@127.0.0.1:27017"


ConvertAndReplace() {
  for d in *
  do
  echo "Current file path: "; pwd

  filename=$(basename -- "$d")
  echo "Current FULL file name: $filename"

  extension=${filename##*.}
  echo "Current file extension: $extension"


    if [ -d "$d" ]
    then
      echo "Folder was found we cd now into folder: $d"
      printf "\n Current file path before we cd: "; pwd
      pushd "$d"
      ConvertAndReplace
      popd
    else
      for f in *.bson;
      do
        echo "File was found.. Current path: "; pwd

        JSONfile="$f.json"
        echo "New JSON file is called: $JSONfile"

        bsondump --pretty "$f" > $JSONfile
        sed -i -E "s/amazon/blaa/g" $JSONfile
      done
    fi

  done
}


# ---- START SCRIPT ----
# remove old dump folder
rm -rf dump

# create new dumb
mongodump --uri $MongoDBURI

# first convert BSON to JSON and after this replace s3 links with new gcloud links
cd dump
ConvertAndReplace
```





<br><br><br><br>



## Mongodumb
- Export Database/Collections

<br><br>

#### Export specific database with all collections to .bson
```bash
# method #1
mongodump --host xx.xxx.xx.xx --port 27017 --db your_db_name --username your_user_name --password your_password --out /target/folder/path

# method #2 - srv link
mongodump --uri "mongodb://userhere:passwordhere@127.0.0.1:27017" -d testdb
```


<br><br>

#### Export all databases to .bson
```bash
# method #1
mongodump -h 127.0.0.1:27017 -u sampleuser -p samplepw # If you get auth error you maybe use this flag: --authenticationDatabase admin

# method #2 - srv link
mongodump --uri "mongodb://userhere:passwordhere@127.0.0.1:27017"
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


#### show current database
```bash
db
```

<br><br>


#### switch database
```bash
use databasenamehere
databasenamehere.myCollection.insertOne( { x: 1 } );
```

<br><br>































<br><br>

____________________________________________________
____________________________________________________

<br><br>

# Connection (http://mongodb.github.io/node-mongodb-native/2.1/reference/connecting/connection-settings/)
- Always handle the **serverSelectionTimeout** in your error catch to check where any server gets down or when any problems happen
```javascript
let myDB;
var MongoClient = require('mongodb').MongoClient;




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
        
        const collection = myDB.collection('yourcollectionname');

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

# Database References

<br><br>

## $ref
- The $ref field holds the name of the collection where the referenced document resides.


<br><br>

## $id
- The $id field contains the value of the _id field in the referenced document.

<br><br>

## $db
- Contains the name of the database where the referenced document resides.




































































<br><br>

____________________________________________________
____________________________________________________

<br><br>

# Operators

## Logical Query Operators

#### Comparison Query Operators (https://docs.mongodb.com/manual/reference/operator/query-comparison/)

<br><br>
____________________________________________________
<br><br>
- $eq	Matches values that are equal to a specified value. (https://docs.mongodb.com/manual/reference/operator/aggregation/eq/)
- Syntax:
```javascript
{ $eq: [ <expression1>, <expression2> ] }
```
- Example:
```javascript
/* // Source collection:
[
  { "_id" : 1, "item" : "abc1", description: "product 1", qty: 300 },
  { "_id" : 2, "item" : "abc2", description: "product 2", qty: 200 },
  { "_id" : 3, "item" : "xyz1", description: "product 3", qty: 250 },
  { "_id" : 4, "item" : "VWZ1", description: "product 4", qty: 300 },
  { "_id" : 5, "item" : "VWZ2", description: "product 5", qty: 180 },
]
*/

const pipeline = [
     {
       $project:
          {
            item: 1,
            qty: 1,
            qtyEq250: { $eq: [ "$qty", 250 ] },
            _id: 0
          }
     }
   ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
[
  { "item" : "abc1", "qty" : 300, "qtyEq250" : false },
  { "item" : "abc2", "qty" : 200, "qtyEq250" : false },
  { "item" : "xyz1", "qty" : 250, "qtyEq250" : true },
  { "item" : "VWZ1", "qty" : 300, "qtyEq250" : false },
  { "item" : "VWZ2", "qty" : 180, "qtyEq250" : false },
]
*/
```


<br><br>
____________________________________________________
<br><br>
- $gt	Matches values that are greater than a specified value. (https://docs.mongodb.com/manual/reference/operator/aggregation/gt/)


<br><br>
____________________________________________________
<br><br>
- $gte	Matches values that are greater than or equal to a specified value. (https://docs.mongodb.com/manual/reference/operator/aggregation/gte/)



<br><br>
____________________________________________________
<br><br>
- $in	Matches any of the values specified in an array. Or in other words query array. (https://docs.mongodb.com/manual/reference/operator/aggregation/in/)
- Syntax:
```javascript
{ $in: [ <expression>, <array expression> ] }
```
- Example:
```javascript
/* // Source collection:
[
  { "_id" : 1, "location" : "24th Street", "in_stock" : [ "apples", "oranges", "bananas" ] },
  { "_id" : 2, "location" : "36th Street", "in_stock" : [ "bananas", "pears", "grapes" ] },
  { "_id" : 3, "location" : "82nd Street", "in_stock" : [ "cantaloupes", "watermelons", "apples" ] },
]
*/

const pipeline = [
  {
    $project: {
      "store location" : "$location",
      "has bananas" : {
        $in: [ "bananas", "$in_stock" ]
      }
    }
  }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
[
  { "_id" : 1, "store location" : "24th Street", "has bananas" : true },
  { "_id" : 2, "store location" : "36th Street", "has bananas" : true },
  { "_id" : 3, "store location" : "82nd Street", "has bananas" : false },
]
*/
```



<br><br>
____________________________________________________
<br><br>
- $lt	Matches values that are less than a specified value. (https://docs.mongodb.com/manual/reference/operator/aggregation/lt/)


<br><br>
____________________________________________________
<br><br>
- $lte	Matches values that are less than or equal to a specified value. (https://docs.mongodb.com/manual/reference/operator/aggregation/lte/)


<br><br>
____________________________________________________
<br><br>
- $ne	Compares two values and returns: true when the values are not equivalent. false when the values are equivalent. (https://docs.mongodb.com/manual/reference/operator/aggregation/ne/)
- Syntax:
```javascript
{ $ne: [ <expression1>, <expression2> ] }
```
- Example:
```javascript
// ---- EXAMPLE #1 ---------
/* // Source collection:
[
  { "_id" : 1, "item" : "abc1", description: "product 1", qty: 300 },
  { "_id" : 2, "item" : "abc2", description: "product 2" },
  { "_id" : 3, "item" : "xyz1", description: "product 3", qty: 250 },
]
*/

// The following operation uses the $ne operator to determine if qty does not equal 250:
const pipeline = [
     {
       $project:
          {
            item: 1,
            qty: 1,
            exist: { $ne: ''},
            _id: 0
          }
     }
   ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
[
  { "item" : "abc1", "qty" : 300, "exist" : true },
  { "item" : "abc2", "qty" : 200, "exist" : false },
  { "item" : "xyz1", "qty" : 250, "exist" : true },
]
*/











// ---- EXAMPLE #2 ---------
/* // Source collection:
[
  { "_id" : 1, "item" : "abc1", description: "product 1", qty: 300 },
  { "_id" : 2, "item" : "abc2", description: "product 2", qty: 200 },
  { "_id" : 3, "item" : "xyz1", description: "product 3", qty: 250 },
  { "_id" : 4, "item" : "VWZ1", description: "product 4", qty: 300 },
  { "_id" : 5, "item" : "VWZ2", description: "product 5", qty: 180 },
]
*/

// The following operation uses the $ne operator to determine if qty does not equal 250:
const pipeline = [
     {
       $project:
          {
            item: 1,
            qty: 1,
            qtyNe250: { $ne: [ "$qty", 250 ] },
            _id: 0
          }
     }
   ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
[
  { "item" : "abc1", "qty" : 300, "qtyNe250" : true },
  { "item" : "abc2", "qty" : 200, "qtyNe250" : true },
  { "item" : "xyz1", "qty" : 250, "qtyNe250" : false },
  { "item" : "VWZ1", "qty" : 300, "qtyNe250" : true },
  { "item" : "VWZ2", "qty" : 180, "qtyNe250" : true },
]
*/
```



<br><br>
____________________________________________________
<br><br>
- $nin	Matches none of the values specified in an array. (https://docs.mongodb.com/manual/reference/operator/query/nin/)













<br><br>
____________________________________________________
____________________________________________________
<br><br>







#### Logical Query Operators (https://docs.mongodb.com/manual/reference/operator/query-logical/)
- $and	Joins query clauses with a logical AND returns all documents that match the conditions of both clauses. (https://docs.mongodb.com/manual/reference/operator/query/and/)
```javascript
/*
This query will select all documents in the inventory collection where:
- the price field value is not equal to 1.99 and
- the price field exists.
*/
const query = {$and: [{price: {$ne: 1.99}}, {price: {$exists: true}}]};

// callback
collection.findOne(query, (e, docs) => { /* .. */ });

// async
const r = await collection.findOne(query)
```

<br><br>
____________________________________________________
<br><br>
- $not	Inverts the effect of a query expression and returns documents that do not match the query expression. (https://docs.mongodb.com/manual/reference/operator/query/not/)


<br><br>
____________________________________________________
<br><br>
- $nor	Joins query clauses with a logical NOR returns all documents that fail to match both clauses. (https://docs.mongodb.com/manual/reference/operator/query/nor/)


<br><br>
____________________________________________________
<br><br>
- $or	Joins query clauses with a logical OR returns all documents that match the conditions of either clause. (https://docs.mongodb.com/manual/reference/operator/query/or/)
- Syntax:
```javascript
{$or: [ { <expression1> }, { <expression2> }, ... , { <expressionN> } ]}
```
- Example:
```javascript
const query = {$or: [{quantity: {$lt: 20}}, {price: 10}]};

// callback
collection.find(query).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.find(query).toArray({});
```








<br><br>
____________________________________________________
____________________________________________________
<br><br>






#### Element Query Operators (https://docs.mongodb.com/manual/reference/operator/query-element/)
- $exists	Matches documents that have the specified field. (https://docs.mongodb.com/manual/reference/operator/query/exists/)
```javascript
const query = {"payload.discount": {$exists: true}};

// callback
collection.findOne(query, (e, docs) => { /* .. */ });

// async
const r = await collection.findOne(query)
```


<br><br>
____________________________________________________
<br><br>
- $type	Selects documents if a field is of the specified type. (https://docs.mongodb.com/manual/reference/operator/query/type/)
- Syntax:
```javascript
{ field: { $type: <BSON type> } }

// or 

{ field: { $type: [ <BSON type1> , <BSON type2>, ... ] } }
```
- Example:
```javascript
/* // Source collection:
[
      { "_id" : 1, name : "Alice King" , classAverage : 87.333333333333333 },
      { "_id" : 2, name : "Bob Jenkins", classAverage : "83.52" },
      { "_id" : 3, name : "Cathy Hart", classAverage: "94.06" },
      { "_id" : 4, name : "Drew Williams" , classAverage : NumberInt("93") }
   ]
*/


db.grades.find( { "classAverage" : { $type : [ 2 , 1 ] } } );
db.grades.find( { "classAverage" : { $type : [ "string" , "double" ] } } );

/* operation will return:
[
  { "_id" : 1, "name" : "Alice King", "classAverage" : 87.33333333333333 },
  { "_id" : 2, "name" : "Bob Jenkins", "classAverage" : "83.52" },
  { "_id" : 3, "name" : "Cathy Hart", "classAverage" : "94.06" },
]
*/
```






<br><br>
____________________________________________________
____________________________________________________
<br><br>





#### Evaluation Query Operators (https://docs.mongodb.com/manual/reference/operator/query-evaluation/)
- $expr	Allows use of aggregation expressions within the query language. (https://docs.mongodb.com/manual/reference/operator/query/expr/)


<br><br>
____________________________________________________
<br><br>
- $jsonSchema	Validate documents against the given JSON Schema. (https://docs.mongodb.com/manual/reference/operator/query/jsonSchema/)


<br><br>
____________________________________________________
<br><br>
- $mod	Performs a modulo operation on the value of a field and selects documents with a specified result. (https://docs.mongodb.com/manual/reference/operator/query/mod/)


<br><br>
____________________________________________________
<br><br>
- $regex	Selects documents where values match a specified regular expression. (https://docs.mongodb.com/manual/reference/operator/query/regex/)
- **input**	- An expression that resolves to an array.
- **as** - Optional. A name for the variable that represents each individual element of the input array. If no name is specified, the variable name defaults to this.
- **in** - An expression that is applied to each element of the input array. The expression references each element individually with the variable name specified in as.
```javascript
/* Our collection looks like this:
  {"_id": 1, "item": "word with spaces"}
  {"_id": 2, "item": "wordwithoutspaces"}
*/

// match single words without white spaces
const pipeline = [{$match: {'title': {'$regex': /^[^\s]+$/ }}}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});


/* operation will return:
  {"_id" : 2, "item" : "wordwithoutspaces"}
*/
```



<br><br>
____________________________________________________
<br><br>
- **$text**	- Performs a text search on the content of the fields indexed with a text index. (https://docs.mongodb.com/manual/reference/operator/query/text/)
- In easy words when you use **.createIndex()** and create a **text index** on specific field you can use **$text** to search data on those fields.
- Syntax:
```javascript
{
  $text:
    {
      $search: <string>,
      $language: <string>,
      $caseSensitive: <boolean>,
      $diacriticSensitive: <boolean>
    }
}
```
- Options:
```javascript
/*
- $search | string | A string of terms that MongoDB parses and uses to query the text index. MongoDB performs a logical OR search of the terms unless specified as a phrase. See Behavior for more information on the field.

- $language | string | Optional. The language that determines the list of stop words for the search and the rules for the stemmer and tokenizer. If not specified, the search uses the default language of the index. For supported languages, see Text Search Languages.

- $caseSensitive | boolean | Optional. A boolean flag to enable or disable case sensitive search. Defaults to false; i.e. the search defers to the case insensitivity of the text index.

- $diacriticSensitive | boolean | Optional. A boolean flag to enable or disable diacritic sensitive search against version 3 text indexes. Defaults to false; i.e. the search defers to the diacritic insensitivity of the text index.
*/
```
- Example:
```javascript
/* // source collection
[
     { _id: 1, subject: "coffee", author: "xyz", views: 50 },
     { _id: 2, subject: "Coffee Shopping", author: "efg", views: 5 },
     { _id: 3, subject: "Baking a cake", author: "abc", views: 90  },
     { _id: 4, subject: "baking", author: "xyz", views: 100 },
     { _id: 5, subject: "Café Con Leche", author: "abc", views: 200 },
     { _id: 6, subject: "Сырники", author: "jkl", views: 80 },
     { _id: 7, subject: "coffee and cream", author: "efg", views: 10 },
     { _id: 8, subject: "Cafe con Leche", author: "xyz", views: 10 }
]
*/

// The following query specifies a $search string of coffee:
const query = {$text: {$search: "coffee"}};

// callback
collection.find(query).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.find(query).toArray({});

/* operation will return:
[
  { "_id" : 2, "subject" : "Coffee Shopping", "author" : "efg", "views" : 5 },
  { "_id" : 7, "subject" : "coffee and cream", "author" : "efg", "views" : 10 },
  { "_id" : 1, "subject" : "coffee", "author" : "xyz", "views" : 50 },
]
*/











// ---- EXAMPLE #2 - Match Any of the Search Terms ----

// The following query specifies a $search string of three terms delimited by space, "bake coffee cake":
collection.find( { $text: { $search: "bake coffee cake" } } )

/*  // result:
[
  { "_id" : 2, "subject" : "Coffee Shopping", "author" : "efg", "views" : 5 },
  { "_id" : 7, "subject" : "coffee and cream", "author" : "efg", "views" : 10 },
  { "_id" : 1, "subject" : "coffee", "author" : "xyz", "views" : 50 },
  { "_id" : 3, "subject" : "Baking a cake", "author" : "abc", "views" : 90 },
  { "_id" : 4, "subject" : "baking", "author" : "xyz", "views" : 100 },
]
*/











// ---- EXAMPLE #3 - Search for a Phrase ----

// The following query searches for the phrase coffee shop:
collection.find( { $text: { $search: "\"coffee shop\"" } } )

/*  // result:
{ "_id" : 2, "subject" : "Coffee Shopping", "author" : "efg", "views" : 5 }
*/















// ---- EXAMPLE #4 - Exclude Documents That Contain a Term ----

// The following query searches for the phrase coffee shop:
collection.find( { $text: { $search: "coffee -shop" } } )

/*  // result:
[
  { "_id" : 7, "subject" : "coffee and cream", "author" : "efg", "views" : 10 },
  { "_id" : 1, "subject" : "coffee", "author" : "xyz", "views" : 50 },
]
*/
```



<br><br>
____________________________________________________
<br><br>
- $where	Matches documents that satisfy a JavaScript expression. (https://docs.mongodb.com/manual/reference/operator/query/where/)









<br><br>
____________________________________________________
____________________________________________________
<br><br>




#### Geospatial Query Operators (https://docs.mongodb.com/manual/reference/operator/query-geospatial/)
- $geoIntersects	Selects geometries that intersect with a GeoJSON geometry. The 2dsphere index supports $geoIntersects. (https://docs.mongodb.com/manual/reference/operator/query/geoIntersects/)


<br><br>
____________________________________________________
<br><br>
- $geoWithin	Selects geometries within a bounding GeoJSON geometry. The 2dsphere and 2d indexes support $geoWithin. (https://docs.mongodb.com/manual/reference/operator/query/geoWithin/)


<br><br>
____________________________________________________
<br><br>
- $near	Returns geospatial objects in proximity to a point. Requires a geospatial index. The 2dsphere and 2d indexes support $near. (https://docs.mongodb.com/manual/reference/operator/query/near/)


<br><br>
____________________________________________________
<br><br>
- $nearSphere	Returns geospatial objects in proximity to a point on a sphere. Requires a geospatial index. The 2dsphere and 2d indexes support $nearSphere. (https://docs.mongodb.com/manual/reference/operator/query/nearSphere/)









<br><br>
____________________________________________________
____________________________________________________
<br><br>






#### Array Query Operators (https://docs.mongodb.com/manual/reference/operator/query-array/)
- $all	Matches arrays that contain all elements specified in the query. (https://docs.mongodb.com/manual/reference/operator/query/all/)


<br><br>
____________________________________________________
<br><br>
- $elemMatch	Selects documents if element in the array field matches all the specified $elemMatch conditions. (https://docs.mongodb.com/manual/reference/operator/query/elemMatch/)




<br><br>
____________________________________________________
<br><br>
- $size	Selects documents if the array field is a specified size. (https://docs.mongodb.com/manual/reference/operator/query/size/)
- The $size operator matches any array with the number of elements specified by the argument. For example:
- Example:
```javascript
const query = {field: {$size: 2}};

// callback
collection.find(query).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.find(query).toArray({});
```







<br><br>
____________________________________________________
____________________________________________________
<br><br>









#### Bitwise Query Operators (https://docs.mongodb.com/manual/reference/operator/query-bitwise/)
- $bitsAllClear	Matches numeric or binary values in which a set of bit positions all have a value of 0. (https://docs.mongodb.com/manual/reference/operator/query/bitsAllClear/)


<br><br>
____________________________________________________
<br><br>
- $bitsAllSet	Matches numeric or binary values in which a set of bit positions all have a value of 1. (https://docs.mongodb.com/manual/reference/operator/query/bitsAllSet/)


<br><br>
____________________________________________________
<br><br>
- $bitsAnyClear	Matches numeric or binary values in which any bit from a set of bit positions has a value of 0. (https://docs.mongodb.com/manual/reference/operator/query/bitsAnyClear/)


<br><br>
____________________________________________________
<br><br>
- $bitsAnySet	Matches numeric or binary values in which any bit from a set of bit positions has a value of 1. (https://docs.mongodb.com/manual/reference/operator/query/bitsAnySet/)















<br><br>
____________________________________________________
____________________________________________________
<br><br>










## Aggregation Pipeline Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/)




<br><br>

#### Aggregation Pipeline Stages
- $addFields	Adds new fields to documents. Similar to $project, $addFields reshapes each document in the stream; specifically, by adding new fields to output documents that contain both the existing fields from the input documents and the newly added fields. (https://docs.mongodb.com/manual/reference/operator/aggregation/addFields/#pipe._S_addFields)
- It is similiar to projection but $addFields only allows you to modify the incoming pipeline documents. The nicest difference is that with projection your manually have to define all fields that you want to include to the results. With very big objects this can be a pain. Instead you can use $addFields to quickly add new fields and still recieve all other fields in your result.
- Syntax:
```javascript
{ $addFields: { <newField>: <expression>, ... } }
```
- Example:
```javascript
/* // Source collection:
{
  _id: 1,
  student: "Maya",
  homework: [ 10, 5, 10 ],
  quiz: [ 10, 8 ],
  extraCredit: 0
}
{
  _id: 2,
  student: "Ryan",
  homework: [ 5, 6, 5 ],
  quiz: [ 8, 8 ],
  extraCredit: 8
}
*/

const pipeline = [
   {
     $addFields: {
       totalHomework: { $sum: "$homework" } ,
       totalQuiz: { $sum: "$quiz" }
     }
   },
   {
     $addFields: { totalScore:
       { $add: [ "$totalHomework", "$totalQuiz", "$extraCredit" ] } }
   }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
{
  "_id" : 1,
  "student" : "Maya",
  "homework" : [ 10, 5, 10 ],
  "quiz" : [ 10, 8 ],
  "extraCredit" : 0,
  "totalHomework" : 25,
  "totalQuiz" : 18,
  "totalScore" : 43
}
{
  "_id" : 2,
  "student" : "Ryan",
  "homework" : [ 5, 6, 5 ],
  "quiz" : [ 8, 8 ],
  "extraCredit" : 8,
  "totalHomework" : 16,
  "totalQuiz" : 16,
  "totalScore" : 40
}
*/
```


<br><br>
____________________________________________________
<br><br>
- $bucket	Categorizes incoming documents into groups, called buckets, based on a specified expression and bucket boundaries. (https://docs.mongodb.com/manual/reference/operator/aggregation/bucket/#pipe._S_bucket)

<br><br>
- Guides:
<br> https://www.youtube.com/watch?v=jGDLtd0zyro

<br><br>
- Syntax:
```javascript
{
  $bucket: {
      groupBy: <expression>,
      boundaries: [ <lowerbound1>, <lowerbound2>, ... ],
      default: <literal>,
      output: {
         <output1>: { <$accumulator expression> },
         ...
         <outputN>: { <$accumulator expression> }
      }
   }
}
```
- Options:
```javascript
- groupBy | expression | An expression to group documents by. To specify a field path, prefix the field name with a dollar sign $ and enclose it in quotes.


- boundaries | array | An array of values based on the groupBy expression that specify the boundaries for each bucket. Each adjacent pair of values acts as the inclusive lower boundary and the exclusive upper boundary for the bucket. You must specify at least two boundaries.
- In easy words you can specify the range of fields
- All array values must have the same type or you get an error.
- Must specifiy atleast 2 values


- default	| literal	| Optional. A literal that specifies the _id of an additional bucket that contains all documents whose groupBy expression result does not fall into a bucket specified by boundaries.
- In easy words if your boundaries does not match a field you can use default to prevent errors. (https://youtu.be/jGDLtd0zyro?t=244)


- output | document | Optional. A document that specifies the fields to include in the output documents in addition to the _id field. To specify the field to include, you must use accumulator expressions.
- without output count will be inserted by default. If output ist set then count will be removed.

```
- Example:
```javascript
// ---- example1 ----
https://youtu.be/jGDLtd0zyro?t=82













// ---- example2 ----
/* // Source collection:
[
{ "_id" : 1, "last_name" : "Bernard", "first_name" : "Emil", "year_born" : 1868, "year_died" : 1941, "nationality" : "France" },
  { "_id" : 2, "last_name" : "Rippl-Ronai", "first_name" : "Joszef", "year_born" : 1861, "year_died" : 1927, "nationality" : "Hungary" },
  { "_id" : 3, "last_name" : "Ostroumova", "first_name" : "Anna", "year_born" : 1871, "year_died" : 1955, "nationality" : "Russia" },
  { "_id" : 4, "last_name" : "Van Gogh", "first_name" : "Vincent", "year_born" : 1853, "year_died" : 1890, "nationality" : "Holland" },
  { "_id" : 5, "last_name" : "Maurer", "first_name" : "Alfred", "year_born" : 1868, "year_died" : 1932, "nationality" : "USA" },
  { "_id" : 6, "last_name" : "Munch", "first_name" : "Edvard", "year_born" : 1863, "year_died" : 1944, "nationality" : "Norway" },
  { "_id" : 7, "last_name" : "Redon", "first_name" : "Odilon", "year_born" : 1840, "year_died" : 1916, "nationality" : "France" },
  { "_id" : 8, "last_name" : "Diriks", "first_name" : "Edvard", "year_born" : 1855, "year_died" : 1930, "nationality" : "Norway" },
]
*/

// The following operation groups the documents into buckets according to the year_born field and filters based on the count of documents in the buckets:
const pipeline = [
  // First Stage
  {
    $bucket: {
      groupBy: "$year_born",                        // Field to group by
      boundaries: [ 1840, 1850, 1860, 1870, 1880 ], // Boundaries for the buckets
      default: "Other",                             // Bucket id for documents which do not fall into a bucket
      output: {                                     // Output for each bucket
        "count": { $sum: 1 },
        "artists" :
          {
            $push: {
              "name": { $concat: [ "$first_name", " ", "$last_name"] },
              "year_born": "$year_born"
            }
          }
      }
    }
  },
  // Second Stage
  {
    $match: { count: {$gt: 3} }
  }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* First Stage:
The $bucket stage groups the documents into buckets by the year_born field. The buckets have the following boundaries:

- [1840, 1850) with inclusive lowerbound 1840 and exclusive upper bound 1850.
- [1850, 1860) with inclusive lowerbound 1850 and exclusive upper bound 1860.
- [1860, 1870) with inclusive lowerbound 1860 and exclusive upper bound 1870.
- [1870, 1880) with inclusive lowerbound 1870 and exclusive upper bound 1880.
- If a document did not contain the year_born field or its year_born field was outside the ranges above, it would be placed in the default bucket with the _id value "Other".


This stage passes the following documents to the next stage:
{ "_id" : 1840, "count" : 1, "artists" : [ { "name" : "Odilon Redon", "year_born" : 1840 } ] }

{ "_id" : 1850, "count" : 2, "artists" : [ { "name" : "Vincent Van Gogh", "year_born" : 1853 },
                                           { "name" : "Edvard Diriks", "year_born" : 1855 } ] }

{ "_id" : 1860, "count" : 4, "artists" : [ { "name" : "Emil Bernard", "year_born" : 1868 },
                                           { "name" : "Joszef Rippl-Ronai", "year_born" : 1861 },
                                           { "name" : "Alfred Maurer", "year_born" : 1868 },
                                           { "name" : "Edvard Munch", "year_born" : 1863 } ] }

{ "_id" : 1870, "count" : 1, "artists" : [ { "name" : "Anna Ostroumova", "year_born" : 1871 } ] }
*/



/* Second Stage:
The $match stage filters the output from the previous stage to only return buckets which contain more than 3 documents.
The operation returns the following document:
{ "_id" : 1860, "count" : 4, "artists" :
  [
    { "name" : "Emil Bernard", "year_born" : 1868 },
    { "name" : "Joszef Rippl-Ronai", "year_born" : 1861 },
    { "name" : "Alfred Maurer", "year_born" : 1868 },
    { "name" : "Edvard Munch", "year_born" : 1863 }
  ]
}
*/



































// ---- EXAMPLE #3 - Use $bucket with $facet to Bucket by Multiple Fields ----

/* // Source collection:
[
  { "_id" : 1, "title" : "The Pillars of Society", "artist" : "Grosz", "year" : 1926,
      "price" : NumberDecimal("199.99") },
  { "_id" : 2, "title" : "Melancholy III", "artist" : "Munch", "year" : 1902,
      "price" : NumberDecimal("280.00") },
  { "_id" : 3, "title" : "Dancer", "artist" : "Miro", "year" : 1925,
      "price" : NumberDecimal("76.04") },
  { "_id" : 4, "title" : "The Great Wave off Kanagawa", "artist" : "Hokusai",
      "price" : NumberDecimal("167.30") },
  { "_id" : 5, "title" : "The Persistence of Memory", "artist" : "Dali", "year" : 1931,
      "price" : NumberDecimal("483.00") },
  { "_id" : 6, "title" : "Composition VII", "artist" : "Kandinsky", "year" : 1913,
      "price" : NumberDecimal("385.00") },
  { "_id" : 7, "title" : "The Scream", "artist" : "Munch", "year" : 1893
      /* No price*/ },
  { "_id" : 8, "title" : "Blue Flower", "artist" : "O'Keefe", "year" : 1918,
      "price" : NumberDecimal("118.42") }
]
*/


// You can use the $facet stage to perform multiple $bucket aggregations in a single stage.
const pipeline = [
  {
    $facet: {                               // Top-level $facet stage
      "price": [                            // Output field 1
        {
          $bucket: {
              groupBy: "$price",            // Field to group by
              boundaries: [ 0, 200, 400 ],  // Boundaries for the buckets
              default: "Other",             // Bucket id for documents which do not fall into a bucket
              output: {                     // Output for each bucket
                "count": { $sum: 1 },
                "artwork" : { $push: { "title": "$title", "price": "$price" } },
                "averagePrice": { $avg: "$price" }
              }
          }
        }
      ],
      "year": [                                      // Output field 2
        {
          $bucket: {
            groupBy: "$year",                        // Field to group by
            boundaries: [ 1890, 1910, 1920, 1940 ],  // Boundaries for the buckets
            default: "Unknown",                      // Bucket id for documents which do not fall into a bucket
            output: {                                // Output for each bucket
              "count": { $sum: 1 },
              "artwork": { $push: { "title": "$title", "year": "$year" } }
            }
          }
        }
      ]
    }
  }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
[
{
  "price" : [ // Output of first facet
    {
      "_id" : 0,
      "count" : 4,
      "artwork" : [
        { "title" : "The Pillars of Society", "price" : NumberDecimal("199.99") },
        { "title" : "Dancer", "price" : NumberDecimal("76.04") },
        { "title" : "The Great Wave off Kanagawa", "price" : NumberDecimal("167.30") },
        { "title" : "Blue Flower", "price" : NumberDecimal("118.42") }
      ],
      "averagePrice" : NumberDecimal("140.4375")
    },
    {
      "_id" : 200,
      "count" : 2,
      "artwork" : [
        { "title" : "Melancholy III", "price" : NumberDecimal("280.00") },
        { "title" : "Composition VII", "price" : NumberDecimal("385.00") }
      ],
      "averagePrice" : NumberDecimal("332.50")
    },
    {
      // Includes documents without prices and prices greater than 400
      "_id" : "Other",
      "count" : 2,
      "artwork" : [
        { "title" : "The Persistence of Memory", "price" : NumberDecimal("483.00") },
        { "title" : "The Scream" }
      ],
      "averagePrice" : NumberDecimal("483.00")
    }
  ],
  "year" : [ // Output of second facet
    {
      "_id" : 1890,
      "count" : 2,
      "artwork" : [
        { "title" : "Melancholy III", "year" : 1902 },
        { "title" : "The Scream", "year" : 1893 }
      ]
    },
    {
      "_id" : 1910,
      "count" : 2,
      "artwork" : [
        { "title" : "Composition VII", "year" : 1913 },
        { "title" : "Blue Flower", "year" : 1918 }
      ]
    },
    {
      "_id" : 1920,
      "count" : 3,
      "artwork" : [
        { "title" : "The Pillars of Society", "year" : 1926 },
        { "title" : "Dancer", "year" : 1925 },
        { "title" : "The Persistence of Memory", "year" : 1931 }
      ]
    },
    {
      // Includes documents without a year
      "_id" : "Unknown",
      "count" : 1,
      "artwork" : [
        { "title" : "The Great Wave off Kanagawa" }
      ]
    }
  ]
}
]
*/
```



<br><br>
____________________________________________________
<br><br>
- $bucketAuto	Categorizes incoming documents into a specific number of groups, called buckets, based on a specified expression. Bucket boundaries are automatically determined in an attempt to evenly distribute the documents into the specified number of buckets. (https://docs.mongodb.com/manual/reference/operator/aggregation/bucketAuto/#pipe._S_bucketAuto)
- Guides:
<br> https://www.youtube.com/watch?v=zDtjjNC2yng

<br><br>
- Syntax:
```javascript
{
  $bucketAuto: {
      groupBy: <expression>,
      buckets: <number>,
      output: {
         <output1>: { <$accumulator expression> },
         ...
      }
      granularity: <string>
  }
}
```
- Options:
```javascript
groupBy	| expression | An expression to group documents by. To specify a field path, prefix the field name with a dollar sign $ and enclose it in quotes.


buckets	| integer	| A positive 32-bit integer that specifies the number of buckets into which input documents are grouped.


output | document	| Optional. A document that specifies the fields to include in the output documents in addition to the _id field. To specify the field to include, you must use accumulator expressions:


granularity	| string	| Optional. A string that specifies the preferred number series to use to ensure that the calculated boundary edges end on preferred round numbers or their powers of 10.
- requires the expression to groupBy to resolve a numeric value
```
- Example
```javascript
// ---- EXAMPLE #1 - Single Facet Aggregation ----

/* // source collection:
[
  { "_id" : 1, "title" : "The Pillars of Society", "artist" : "Grosz", "year" : 1926,
    "price" : NumberDecimal("199.99"),
    "dimensions" : { "height" : 39, "width" : 21, "units" : "in" } },
{ "_id" : 2, "title" : "Melancholy III", "artist" : "Munch", "year" : 1902,
    "price" : NumberDecimal("280.00"),
    "dimensions" : { "height" : 49, "width" : 32, "units" : "in" } },
{ "_id" : 3, "title" : "Dancer", "artist" : "Miro", "year" : 1925,
    "price" : NumberDecimal("76.04"),
    "dimensions" : { "height" : 25, "width" : 20, "units" : "in" } },
{ "_id" : 4, "title" : "The Great Wave off Kanagawa", "artist" : "Hokusai",
    "price" : NumberDecimal("167.30"),
    "dimensions" : { "height" : 24, "width" : 36, "units" : "in" } },
{ "_id" : 5, "title" : "The Persistence of Memory", "artist" : "Dali", "year" : 1931,
    "price" : NumberDecimal("483.00"),
    "dimensions" : { "height" : 20, "width" : 24, "units" : "in" } },
{ "_id" : 6, "title" : "Composition VII", "artist" : "Kandinsky", "year" : 1913,
    "price" : NumberDecimal("385.00"),
    "dimensions" : { "height" : 30, "width" : 46, "units" : "in" } },
{ "_id" : 7, "title" : "The Scream", "artist" : "Munch",
    "price" : NumberDecimal("159.00"),
    "dimensions" : { "height" : 24, "width" : 18, "units" : "in" } },
{ "_id" : 8, "title" : "Blue Flower", "artist" : "O'Keefe", "year" : 1918,
    "price" : NumberDecimal("118.42"),
    "dimensions" : { "height" : 24, "width" : 20, "units" : "in" } },
]
*/

// In the following operation, input documents are grouped into four buckets according to the values in the price field:
const pipeline = [
   {
     $bucketAuto: {
         groupBy: "$price",
         buckets: 4
     }
   }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
[
{
  "_id" : {
    "min" : NumberDecimal("76.04"),
    "max" : NumberDecimal("159.00")
  },
  "count" : 2
},
{
  "_id" : {
    "min" : NumberDecimal("159.00"),
    "max" : NumberDecimal("199.99")
  },
  "count" : 2
},
{
  "_id" : {
    "min" : NumberDecimal("199.99"),
    "max" : NumberDecimal("385.00")
  },
  "count" : 2
},
{
  "_id" : {
    "min" : NumberDecimal("385.00"),
    "max" : NumberDecimal("483.00")
  },
  "count" : 2
},
]
*/














































// ---- EXAMPLE #2 - Multi-Faceted Aggregation ----

/* // source collection:
[
  { "_id" : 1, "title" : "The Pillars of Society", "artist" : "Grosz", "year" : 1926,
    "price" : NumberDecimal("199.99"),
    "dimensions" : { "height" : 39, "width" : 21, "units" : "in" } },
{ "_id" : 2, "title" : "Melancholy III", "artist" : "Munch", "year" : 1902,
    "price" : NumberDecimal("280.00"),
    "dimensions" : { "height" : 49, "width" : 32, "units" : "in" } },
{ "_id" : 3, "title" : "Dancer", "artist" : "Miro", "year" : 1925,
    "price" : NumberDecimal("76.04"),
    "dimensions" : { "height" : 25, "width" : 20, "units" : "in" } },
{ "_id" : 4, "title" : "The Great Wave off Kanagawa", "artist" : "Hokusai",
    "price" : NumberDecimal("167.30"),
    "dimensions" : { "height" : 24, "width" : 36, "units" : "in" } },
{ "_id" : 5, "title" : "The Persistence of Memory", "artist" : "Dali", "year" : 1931,
    "price" : NumberDecimal("483.00"),
    "dimensions" : { "height" : 20, "width" : 24, "units" : "in" } },
{ "_id" : 6, "title" : "Composition VII", "artist" : "Kandinsky", "year" : 1913,
    "price" : NumberDecimal("385.00"),
    "dimensions" : { "height" : 30, "width" : 46, "units" : "in" } },
{ "_id" : 7, "title" : "The Scream", "artist" : "Munch",
    "price" : NumberDecimal("159.00"),
    "dimensions" : { "height" : 24, "width" : 18, "units" : "in" } },
{ "_id" : 8, "title" : "Blue Flower", "artist" : "O'Keefe", "year" : 1918,
    "price" : NumberDecimal("118.42"),
    "dimensions" : { "height" : 24, "width" : 20, "units" : "in" } },
]
*/

// The following aggregation pipeline groups the documents from the artwork collection into buckets based on price, year, and the calculated area:
const pipeline = [
  {
    $facet: {
      "price": [
        {
          $bucketAuto: {
            groupBy: "$price",
            buckets: 4
          }
        }
      ],
      "year": [
        {
          $bucketAuto: {
            groupBy: "$year",
            buckets: 3,
            output: {
              "count": { $sum: 1 },
              "years": { $push: "$year" }
            }
          }
        }
      ],
      "area": [
        {
          $bucketAuto: {
            groupBy: {
              $multiply: [ "$dimensions.height", "$dimensions.width" ]
            },
            buckets: 4,
            output: {
              "count": { $sum: 1 },
              "titles": { $push: "$title" }
            }
          }
        }
      ]
    }
  }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
{
  "area" : [
    {
      "_id" : { "min" : 432, "max" : 500 },
      "count" : 3,
      "titles" : [
        "The Scream",
        "The Persistence of Memory",
        "Blue Flower"
      ]
    },
    {
      "_id" : { "min" : 500, "max" : 864 },
      "count" : 2,
      "titles" : [
        "Dancer",
        "The Pillars of Society"
      ]
    },
    {
      "_id" : { "min" : 864, "max" : 1568 },
      "count" : 2,
      "titles" : [
        "The Great Wave off Kanagawa",
        "Composition VII"
      ]
    },
    {
      "_id" : { "min" : 1568, "max" : 1568 },
      "count" : 1,
      "titles" : [
        "Melancholy III"
      ]
    }
  ],
  "price" : [
    {
      "_id" : { "min" : NumberDecimal("76.04"), "max" : NumberDecimal("159.00") },
      "count" : 2
    },
    {
      "_id" : { "min" : NumberDecimal("159.00"), "max" : NumberDecimal("199.99") },
      "count" : 2
    },
    {
      "_id" : { "min" : NumberDecimal("199.99"), "max" : NumberDecimal("385.00") },
      "count" : 2 },
    {
      "_id" : { "min" : NumberDecimal("385.00"), "max" : NumberDecimal("483.00") },
      "count" : 2
    }
  ],
  "year" : [
    { "_id" : { "min" : null, "max" : 1913 }, "count" : 3, "years" : [ 1902 ] },
    { "_id" : { "min" : 1913, "max" : 1926 }, "count" : 3, "years" : [ 1913, 1918, 1925 ] },
    { "_id" : { "min" : 1926, "max" : 1931 }, "count" : 2, "years" : [ 1926, 1931 ] }
  ]
}

*/
```


<br><br>
____________________________________________________
<br><br>
- $collStats	Returns statistics regarding a collection or view. (https://docs.mongodb.com/manual/reference/operator/aggregation/collStats/#pipe._S_collStats)



<br><br>
____________________________________________________
<br><br>
- $count	Returns a count of the number of documents at this stage of the aggregation pipeline. (https://docs.mongodb.com/manual/reference/operator/aggregation/count/#pipe._S_count)
- Syntax:
```javascript
{ $count: <string> }
```
- Example
```javascript
/* // source collection:
[
  { "_id" : 1, "subject" : "History", "score" : 88 },
  { "_id" : 2, "subject" : "History", "score" : 92 },
  { "_id" : 3, "subject" : "History", "score" : 97 },
  { "_id" : 4, "subject" : "History", "score" : 71 },
  { "_id" : 5, "subject" : "History", "score" : 79 },
  { "_id" : 6, "subject" : "History", "score" : 83 },
]
*/

// skip first 2 documents in natural order
const pipeline = [
    {
      $match: {
        score: {
          $gt: 80
        }
      }
    },
    {
      $count: "passing_scores"
    }
  ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
{ "passing_scores" : 4 }
*/
```




<br><br>
____________________________________________________
<br><br>
- $facet	Processes multiple aggregation pipelines within a single stage on the same set of input documents. Enables the creation of multi-faceted aggregations capable of characterizing data across multiple dimensions, or facets, in a single stage. (https://docs.mongodb.com/manual/reference/operator/aggregation/facet/#pipe._S_facet)
- Syntax:
```javascript
{ $facet:
   {
      <outputField1>: [ <stage1>, <stage2>, ... ],
      <outputField2>: [ <stage1>, <stage2>, ... ],
      ...

   }
}
```
- Example
```javascript
/* // source collection:
[
{ "_id" : 1, "title" : "The Pillars of Society", "artist" : "Grosz", "year" : 1926,
  "price" : NumberDecimal("199.99"),
  "tags" : [ "painting", "satire", "Expressionism", "caricature" ] }.
{ "_id" : 2, "title" : "Melancholy III", "artist" : "Munch", "year" : 1902,
  "price" : NumberDecimal("280.00"),
  "tags" : [ "woodcut", "Expressionism" ] }.
{ "_id" : 3, "title" : "Dancer", "artist" : "Miro", "year" : 1925,
  "price" : NumberDecimal("76.04"),
  "tags" : [ "oil", "Surrealism", "painting" ] }.
{ "_id" : 4, "title" : "The Great Wave off Kanagawa", "artist" : "Hokusai",
  "price" : NumberDecimal("167.30"),
  "tags" : [ "woodblock", "ukiyo-e" ] }.
{ "_id" : 5, "title" : "The Persistence of Memory", "artist" : "Dali", "year" : 1931,
  "price" : NumberDecimal("483.00"),
  "tags" : [ "Surrealism", "painting", "oil" ] }.
{ "_id" : 6, "title" : "Composition VII", "artist" : "Kandinsky", "year" : 1913,
  "price" : NumberDecimal("385.00"),
  "tags" : [ "oil", "painting", "abstract" ] }.
{ "_id" : 7, "title" : "The Scream", "artist" : "Munch", "year" : 1893,
  "tags" : [ "Expressionism", "painting", "oil" ] }.
{ "_id" : 8, "title" : "Blue Flower", "artist" : "O'Keefe", "year" : 1918,
  "price" : NumberDecimal("118.42"),
  "tags" : [ "abstract", "painting" ] }
]
*/

// skip first 2 documents in natural order
const pipeline = [
  {
    $facet: {
      "categorizedByTags": [
        { $unwind: "$tags" },
        { $sortByCount: "$tags" }
      ],
      "categorizedByPrice": [
        // Filter out documents without a price e.g., _id: 7
        { $match: { price: { $exists: 1 } } },
        {
          $bucket: {
            groupBy: "$price",
            boundaries: [  0, 150, 200, 300, 400 ],
            default: "Other",
            output: {
              "count": { $sum: 1 },
              "titles": { $push: "$title" }
            }
          }
        }
      ],
      "categorizedByYears(Auto)": [
        {
          $bucketAuto: {
            groupBy: "$year",
            buckets: 4
          }
        }
      ]
    }
  }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
{
  "categorizedByYears(Auto)" : [
    // First bucket includes the document without a year, e.g., _id: 4
    { "_id" : { "min" : null, "max" : 1902 }, "count" : 2 },
    { "_id" : { "min" : 1902, "max" : 1918 }, "count" : 2 },
    { "_id" : { "min" : 1918, "max" : 1926 }, "count" : 2 },
    { "_id" : { "min" : 1926, "max" : 1931 }, "count" : 2 }
  ],
  "categorizedByPrice" : [
    {
      "_id" : 0,
      "count" : 2,
      "titles" : [
        "Dancer",
        "Blue Flower"
      ]
    },
    {
      "_id" : 150,
      "count" : 2,
      "titles" : [
        "The Pillars of Society",
        "The Great Wave off Kanagawa"
      ]
    },
    {
      "_id" : 200,
      "count" : 1,
      "titles" : [
        "Melancholy III"
      ]
    },
    {
      "_id" : 300,
      "count" : 1,
      "titles" : [
        "Composition VII"
      ]
    },
    {
      // Includes document price outside of bucket boundaries, e.g., _id: 5
      "_id" : "Other",
      "count" : 1,
      "titles" : [
        "The Persistence of Memory"
      ]
    }
  ],
  "categorizedByTags" : [
    { "_id" : "painting", "count" : 6 },
    { "_id" : "oil", "count" : 4 },
    { "_id" : "Expressionism", "count" : 3 },
    { "_id" : "Surrealism", "count" : 2 },
    { "_id" : "abstract", "count" : 2 },
    { "_id" : "woodblock", "count" : 1 },
    { "_id" : "woodcut", "count" : 1 },
    { "_id" : "ukiyo-e", "count" : 1 },
    { "_id" : "satire", "count" : 1 },
    { "_id" : "caricature", "count" : 1 }
  ]
}
*/
```



<br><br>
____________________________________________________
<br><br>
- $geoNear	Returns an ordered stream of documents based on the proximity to a geospatial point. Incorporates the functionality of $match, $sort, and $limit for geospatial data. The output documents include an additional distance field and can include a location identifier field. (https://docs.mongodb.com/manual/reference/operator/aggregation/geoNear/#pipe._S_geoNear)
- You can only use $geoNear as the first stage of a pipeline.
- You must include the distanceField option. The distanceField option specifies the field that will contain the calculated distance.
- $geoNear requires a geospatial index.
- If you have more than one geospatial index on the collection, use the keys parameter to specify which field to use in the calculation. If you have only one geospatial index, $geoNear implicitly uses the indexed field for the calculation.
- You cannot specify a $near predicate in the query field of the $geoNear stage.
- Views do not support geoNear operations (i.e. $geoNear pipeline stage).
- Syntax:
```javascript
{ $geoNear: { <geoNear options> } }
```
- Options:
```javascript
- near | The point for which to find the closest documents.
- distanceField | The output field that contains the calculated distance. To specify a field within an embedded document, use dot notation.
- spherical | Optional. Determines how MongoDB calculates the distance between two points.
- maxDistance | Optional. The maximum distance from the center point that the documents can be. MongoDB limits the results to those documents that fall within the specified -distance from the center point.
- query | Optional. Limits the results to the documents that match the query. The query syntax is the usual MongoDB read operation query syntax.
- distanceMultiplier | Optional. The factor to multiply all distances returned by the query. For example, use the distanceMultiplier to convert radians, as returned by a spherical query, to kilometers by multiplying by the radius of the Earth.
- includeLocs | Optional. This specifies the output field that identifies the location used to calculate the distance. This option is useful when a location field contains multiple locations. To specify a field within an embedded document, use dot notation.
- uniqueDocs | Optional. If this value is true, the query returns a matching document once, even if more than one of the document’s location fields match the query.
- minDistance | Optional. The minimum distance from the center point that the documents can be. MongoDB limits the results to those documents that fall outside the specified distance from the center point.
- key | Optional. Specify the geospatial indexed field to use when calculating the distance.
```
- Example:
```javascript
/*
Consider a collection places that has a 2dsphere index. The following aggregation uses $geoNear to find documents with a location at most 2 meters from the center [ -73.99279 , 40.719296 ] and category equal to Parks.
*/

const pipeline = [
   {
     $geoNear: {
        near: { type: "Point", coordinates: [ -73.99279 , 40.719296 ] }, // <-- required 
        distanceField: "dist.calculated", // <-- required 
        maxDistance: 2,
        query: { category: "Parks" },
        includeLocs: "dist.location",
        spherical: true // <-- required 
     }
   }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
{
   "_id" : 8,
   "name" : "Sara D. Roosevelt Park",
   "category" : "Parks",
   "location" : {
      "type" : "Point",
      "coordinates" : [ -73.9928, 40.7193 ]
   },
   "dist" : {
      "calculated" : 0.9539931676365992,
      "location" : {
         "type" : "Point",
         "coordinates" : [ -73.9928, 40.7193 ]
      }
   }
}
*/
```


<br><br>
____________________________________________________
<br><br>
- $graphLookup	Performs a recursive search on a collection. To each output document, adds a new array field that contains the traversal results of the recursive search for that document. (https://docs.mongodb.com/manual/reference/operator/aggregation/graphLookup/#pipe._S_graphLookup)
- In easy words it will displays a nested tree of parents and child elements that were definied together
 - Works from Root to Bottom and Bottom to Root.
- Guides:
<br> Understand $graphLookup (https://www.youtube.com/watch?v=weJ4eyIKabM)
<br> Graph Operations Example (https://www.youtube.com/watch?v=zcH6in9H3ME)
<br> maxDepth and depthField (https://www.youtube.com/watch?v=-Oms-ijrizw)
<br> Cross Collection Lookup (https://www.youtube.com/watch?v=Eiu1jXt6g04)
<br> General Considerations (https://www.youtube.com/watch?v=522TDFDfKKU)

<br><br>
- The $graphLookup search process is summarized below:
<br> 1. Input documents flow into the $graphLookup stage of an aggregation operation.
<br> 2. $graphLookup targets the search to the collection designated by the from parameter (see below for full list of search parameters).
<br> 3. For each input document, the search begins with the value designated by startWith.
<br> 4. $graphLookup matches the startWith value against the field designated by connectToField in other documents in the from collection.
<br> 5. For each matching document, $graphLookup takes the value of the connectFromField and checks every document in the from collection for a matching connectToField value. For each match, $graphLookup adds the matching document in the from collection to an array field named by the as parameter. This step continues recursively until no more matching documents are found, or until the operation reaches a recursion depth specified by the maxDepth parameter. $graphLookup then appends the array field to the input document. $graphLookup returns results after completing its search on all input documents.

<br><br>
- **It is recommended to use $allowDiskUse to prevent problems with your memory.**
- **from collection can not be sharded.**

<br><br>
- Syntax:
```javascript
/*
{
   $graphLookup: {
      from: <collection>,
      startWith: <expression>,
      connectFromField: <string>,
      connectToField: <string>,
      as: <string>,
      maxDepth: <number>,
      depthField: <string>,
      restrictSearchWithMatch: <document>
   }
}
*/
```
- Options:
```javascript
/*
- from | Target collection for the $graphLookup operation to search, recursively matching the connectFromField to the connectToField. The from collection cannot be sharded and must be in the same database as any other collections used in the operation. For information, see Sharded Collections.

- startWith | 	Expression that specifies the value of the connectFromField with which to start the recursive search. Optionally, startWith may be array of values, each of which is individually followed through the traversal process.

- connectFromField | Field name whose value $graphLookup uses to recursively match against the connectToField of other documents in the collection. If the value is an array, each element is individually followed through the traversal process.

- connectToField | Field name in other documents against which to match the value of the field specified by the connectFromField parameter.

- as | Name of the array field added to each output document. Contains the documents traversed in the $graphLookup stage to reach the document.

- maxDepth | Optional. This will tell how many layers we want to go down inside of our tree. To only get the root layer set it to 0. If you do cross collection lookup then maxDepth 0 will not be the root and it starts with 1 instead.

- depthField | Optional. Shows how many layers we were go downinside of our tree to reach this object.

- restrictSearchWithMatch | Optional. A document specifying additional conditions for the recursive search. The syntax is identical to query filter syntax. In other words you can say that you want to ignore specific results.
*/
```
- Example:
```javascript
// ---- EXAMPLE #1 - Within a Single Collection ----

/* source collection:
[
  { "_id" : 1, "name" : "Dev" },
  { "_id" : 2, "name" : "Eliot", "reportsTo" : "Dev" },
  { "_id" : 3, "name" : "Ron", "reportsTo" : "Eliot" },
  { "_id" : 4, "name" : "Andrew", "reportsTo" : "Eliot" },
  { "_id" : 5, "name" : "Asya", "reportsTo" : "Ron" },
  { "_id" : 6, "name" : "Dan", "reportsTo" : "Andrew" },
]
*/

// The following $graphLookup operation recursively matches on the reportsTo and name fields in the employees collection, returning the reporting hierarchy for each person:
const pipeline = [
   {
      $graphLookup: {
         from: "employees",
         startWith: "$reportsTo",
         connectFromField: "reportsTo",
         connectToField: "name",
         as: "reportingHierarchy"
      }
   }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
[
{
   "_id" : 1,
   "name" : "Dev",
   "reportingHierarchy" : [ ]
},
{
   "_id" : 2,
   "name" : "Eliot",
   "reportsTo" : "Dev",
   "reportingHierarchy" : [
      { "_id" : 1, "name" : "Dev" }
   ]
},
{
   "_id" : 3,
   "name" : "Ron",
   "reportsTo" : "Eliot",
   "reportingHierarchy" : [
      { "_id" : 1, "name" : "Dev" },
      { "_id" : 2, "name" : "Eliot", "reportsTo" : "Dev" }
   ]
},
{
   "_id" : 4,
   "name" : "Andrew",
   "reportsTo" : "Eliot",
   "reportingHierarchy" : [
      { "_id" : 1, "name" : "Dev" },
      { "_id" : 2, "name" : "Eliot", "reportsTo" : "Dev" }
   ]
},
{
   "_id" : 5,
   "name" : "Asya",
   "reportsTo" : "Ron",
   "reportingHierarchy" : [
      { "_id" : 1, "name" : "Dev" },
      { "_id" : 2, "name" : "Eliot", "reportsTo" : "Dev" },
      { "_id" : 3, "name" : "Ron", "reportsTo" : "Eliot" }
   ]
},
{
   "_id" : 6,
   "name" : "Dan",
   "reportsTo" : "Andrew",
   "reportingHierarchy" : [
      { "_id" : 1, "name" : "Dev" },
      { "_id" : 2, "name" : "Eliot", "reportsTo" : "Dev" },
      { "_id" : 4, "name" : "Andrew", "reportsTo" : "Eliot" }
   ]
}
]
*/




































// ---- EXAMPLE #2 - Across Multiple Collections ----

/* airports collection:
[
  { "_id" : 0, "airport" : "JFK", "connects" : [ "BOS", "ORD" ] },
  { "_id" : 1, "airport" : "BOS", "connects" : [ "JFK", "PWM" ] },
  { "_id" : 2, "airport" : "ORD", "connects" : [ "JFK" ] },
  { "_id" : 3, "airport" : "PWM", "connects" : [ "BOS", "LHR" ] },
  { "_id" : 4, "airport" : "LHR", "connects" : [ "PWM" ] },
]
*/

/* travelers collection:
[
  { "_id" : 1, "name" : "Dev", "nearestAirport" : "JFK" },
  { "_id" : 2, "name" : "Eliot", "nearestAirport" : "JFK" },
  { "_id" : 3, "name" : "Jeff", "nearestAirport" : "BOS" },
]
*/

// For each document in the travelers collection, the following aggregation operation looks up the nearestAirport value in the airports collection and recursively matches the connects field to the airport field. The operation specifies a maximum recursion depth of 2.
const pipeline = [
   {
      $graphLookup: {
         from: "employees",
         startWith: "$reportsTo",
         connectFromField: "reportsTo",
         connectToField: "name",
         as: "reportingHierarchy"
      }
   }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
[
{
   "_id" : 1,
   "name" : "Dev",
   "nearestAirport" : "JFK",
   "destinations" : [
      { "_id" : 3,
        "airport" : "PWM",
        "connects" : [ "BOS", "LHR" ],
        "numConnections" : NumberLong(2) },
      { "_id" : 2,
        "airport" : "ORD",
        "connects" : [ "JFK" ],
        "numConnections" : NumberLong(1) },
      { "_id" : 1,
        "airport" : "BOS",
        "connects" : [ "JFK", "PWM" ],
        "numConnections" : NumberLong(1) },
      { "_id" : 0,
        "airport" : "JFK",
        "connects" : [ "BOS", "ORD" ],
        "numConnections" : NumberLong(0) }
   ]
},
{
   "_id" : 2,
   "name" : "Eliot",
   "nearestAirport" : "JFK",
   "destinations" : [
      { "_id" : 3,
        "airport" : "PWM",
        "connects" : [ "BOS", "LHR" ],
        "numConnections" : NumberLong(2) },
      { "_id" : 2,
        "airport" : "ORD",
        "connects" : [ "JFK" ],
        "numConnections" : NumberLong(1) },
      { "_id" : 1,
        "airport" : "BOS",
        "connects" : [ "JFK", "PWM" ],
        "numConnections" : NumberLong(1) },
      { "_id" : 0,
        "airport" : "JFK",
        "connects" : [ "BOS", "ORD" ],
        "numConnections" : NumberLong(0) } ]
},
{
   "_id" : 3,
   "name" : "Jeff",
   "nearestAirport" : "BOS",
   "destinations" : [
      { "_id" : 2,
        "airport" : "ORD",
        "connects" : [ "JFK" ],
        "numConnections" : NumberLong(2) },
      { "_id" : 3,
        "airport" : "PWM",
        "connects" : [ "BOS", "LHR" ],
        "numConnections" : NumberLong(1) },
      { "_id" : 4,
        "airport" : "LHR",
        "connects" : [ "PWM" ],
        "numConnections" : NumberLong(2) },
      { "_id" : 0,
        "airport" : "JFK",
        "connects" : [ "BOS", "ORD" ],
        "numConnections" : NumberLong(1) },
      { "_id" : 1,
        "airport" : "BOS",
        "connects" : [ "JFK", "PWM" ],
        "numConnections" : NumberLong(0) }
   ]
}
]
*/































































// ---- EXAMPLE #3 - With a Query Filter ----

/* source collection:
[
{
  "_id" : 1,
  "name" : "Tanya Jordan",
  "friends" : [ "Shirley Soto", "Terry Hawkins", "Carole Hale" ],
  "hobbies" : [ "tennis", "unicycling", "golf" ]
},
{
  "_id" : 2,
  "name" : "Carole Hale",
  "friends" : [ "Joseph Dennis", "Tanya Jordan", "Terry Hawkins" ],
  "hobbies" : [ "archery", "golf", "woodworking" ]
},
{
  "_id" : 3,
  "name" : "Terry Hawkins",
  "friends" : [ "Tanya Jordan", "Carole Hale", "Angelo Ward" ],
  "hobbies" : [ "knitting", "frisbee" ]
},
{
  "_id" : 4,
  "name" : "Joseph Dennis",
  "friends" : [ "Angelo Ward", "Carole Hale" ],
  "hobbies" : [ "tennis", "golf", "topiary" ]
},
{
  "_id" : 5,
  "name" : "Angelo Ward",
  "friends" : [ "Terry Hawkins", "Shirley Soto", "Joseph Dennis" ],
  "hobbies" : [ "travel", "ceramics", "golf" ]
},
{
   "_id" : 6,
   "name" : "Shirley Soto",
   "friends" : [ "Angelo Ward", "Tanya Jordan", "Carole Hale" ],
   "hobbies" : [ "frisbee", "set theory" ]
 },
]
*/


/*
The following aggregation operation uses three stages:
- $match matches on documents with a name field containing the string "Tanya Jordan". Returns one output document.
- $graphLookup connects the output document’s friends field with the name field of other documents in the collection to traverse Tanya Jordan's network of connections. This stage uses the restrictSearchWithMatch parameter to find only documents in which the hobbies array contains golf. Returns one output document.
- $project shapes the output document. The names listed in connections who play golf are taken from the name field of the documents listed in the input document’s golfers array.
*/
const pipeline = [
  { $match: { "name": "Tanya Jordan" } },
  { $graphLookup: {
      from: "people",
      startWith: "$friends",
      connectFromField: "friends",
      connectToField: "name",
      as: "golfers",
      restrictSearchWithMatch: { "hobbies" : "golf" }
    }
  },
  { $project: {
      "name": 1,
      "friends": 1,
      "connections who play golf": "$golfers.name"
    }
  }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
[
{
   "_id" : 1,
   "name" : "Tanya Jordan",
   "friends" : [
      "Shirley Soto",
      "Terry Hawkins",
      "Carole Hale"
   ],
   "connections who play golf" : [
      "Joseph Dennis",
      "Tanya Jordan",
      "Angelo Ward",
      "Carole Hale"
   ]
}
]
*/
```



<br><br>
____________________________________________________
<br><br>
- $group	Groups input documents by a specified identifier expression and applies the accumulator expression(s), if specified, to each group. Consumes all input documents and outputs one document per each distinct group. The output documents only contain the identifier field and, if specified, accumulated fields. (https://docs.mongodb.com/manual/reference/operator/aggregation/group/#pipe._S_group)
- _id is where to specify what incoming documents should be grouped on. **When you got multiple _id with the same value then most operators inside of your group stage will work/combine/compare the collections with the same _id!.**
- Can use all accumulator expressions within $group.
- $group can be used multiple times within a pipeline.
- It may be necessary to sanitize incoming data.
- **_id does not match arrays with different order even when element values are the same**
<br><br>
- Syntax:
```javascript
{
  $group:
    {
      _id: <expression>, // Group By Expression
      <field1>: { <accumulator1> : <expression1> },
      ...
    }
 }
```
- Example:
```javascript
/* Our collection looks like this:
{ "_id" : 1, "item" : "abc", "price" : 10, "quantity" : 2, "date" : ISODate("2014-01-01T08:00:00Z") }
{ "_id" : 2, "item" : "jkl", "price" : 20, "quantity" : 1, "date" : ISODate("2014-02-03T09:00:00Z") }
{ "_id" : 3, "item" : "xyz", "price" : 5, "quantity" : 5, "date" : ISODate("2014-02-03T09:05:00Z") }
{ "_id" : 4, "item" : "abc", "price" : 10, "quantity" : 10, "date" : ISODate("2014-02-15T08:00:00Z") }
{ "_id" : 5, "item" : "xyz", "price" : 5, "quantity" : 10, "date" : ISODate("2014-02-15T09:12:00Z") }
*/


const pipeline = [{
                   $group: {
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
____________________________________________________
<br><br>
- $indexStats	Returns statistics regarding the use of each index for the collection. (https://docs.mongodb.com/manual/reference/operator/aggregation/indexStats/#pipe._S_indexStats)
- $indexStats must be the first stage in a pipeline and may not be used within a $facet.

<br><br>
- Syntax:
```javascript
{ $indexStats: { } }
```
- Example:
```javascript
/* // source collection:
[
  { "_id" : 1, "item" : "abc", "price" : 12, "quantity" : 2, "type": "apparel" },
  { "_id" : 2, "item" : "jkl", "price" : 20, "quantity" : 1, "type": "electronics" },
  { "_id" : 3, "item" : "abc", "price" : 10, "quantity" : 5, "type": "apparel" },
]
*/

// Create the following two indexes on the collection:
db.orders.createIndex( { item: 1, quantity: 1 } )
db.orders.createIndex( { type: 1, item: 1 } )

// Run some queries against the collection:
db.orders.find( { type: "apparel"} )
db.orders.find( { item: "abc" } ).sort( { quantity: 1 } )

// To view statistics on the index use on the orders collection, run the following aggregation operation:
db.orders.aggregate( [ { $indexStats: { } } ] )

/* // result:
{
   "name" : "item_1_quantity_1",
   "key" : { "item" : 1, "quantity" : 1 },
   "host" : "examplehost.local:27018",
   "accesses" : {
      "ops" : NumberLong(1),
      "since" : ISODate("2020-02-10T21:11:23.059Z")
   },
   "shard" : "shardA",      // Available starting in MongoDB 4.2.4 if run on sharded cluster
   "spec" : {               // Available starting in MongoDB 4.2.4
      "v" : 2,
      "key" : { "item" : 1, "quantity" : 1 },
      "name" : "item_1_quantity_1"
   }
}
{
   "name" : "item_1_price_1",
   "key" : { "item" : 1, "price" : 1 },
   "host" : "examplehost.local:27018",
   "accesses" : {
      "ops" : NumberLong(1),
      "since" : ISODate("2020-02-10T21:11:23.233Z")
   },
   "shard" : "shardA",      // Available starting in MongoDB 4.2.4 if run on sharded cluster
   "spec" : {               // Available starting in MongoDB 4.2.4
      "v" : 2,
      "key" : { "item" : 1, "price" : 1 },
      "name" : "item_1_price_1"
   }
}
{
   "name" : "item_1",
   "key" : { "item" : 1 },

   "host" : "examplehost.local:27018",
   "accesses" : {
      "ops" : NumberLong(0),
      "since" : ISODate("2020-02-10T21:11:22.947Z")
   },
   "shard" : "shardA",      // Available starting in MongoDB 4.2.4 if run on sharded cluster
   "spec" : {               // Available starting in MongoDB 4.2.4
      "v" : 2,
      "key" : { "item" : 1 },
      "name" : "item_1"
   }
}
{
   "name" : "_id_",
   "key" : { "_id" : 1 },
   "host" : "examplehost.local:27018",
   "accesses" : {
      "ops" : NumberLong(0),
      "since" : ISODate("2020-02-10T21:11:18.298Z")
   },
   "shard" : "shardA",      // Available starting in MongoDB 4.2.4 if run on sharded cluster
   "spec" : {               // Available starting in MongoDB 4.2.4
      "v" : 2,
      "key" : { "_id" : 1 },
      "name" : "_id_"
   }
}
*/
```



<br><br>
____________________________________________________
<br><br>
- $limit	Passes the first n documents unmodified to the pipeline where n is the specified limit. For each input document, outputs either one document (for the first n documents) or zero documents (after the first n documents). (https://docs.mongodb.com/manual/reference/operator/aggregation/limit/#pipe._S_limit)
```javascript
/* // Our collection looks like this:
[
  { "_id" : 1, "used" : 0, "price" : 10, "quantity" : 2, "date" : ISODate("2014-01-01T08:00:00Z") },
  { "_id" : 2, "used" : 0, "price" : 20, "quantity" : 1, "date" : ISODate("2014-02-03T09:00:00Z") },
  { "_id" : 3, "used" : 0, "price" : 5, "quantity" : 5, "date" : ISODate("2014-02-03T09:05:00Z") },
];
*/

const pipeline = [{$match: { used: 0 }}, {$limit: 2}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
[
  { "_id" : 1, "used" : 0, "price" : 10, "quantity" : 2, "date" : ISODate("2014-01-01T08:00:00Z") },
  { "_id" : 2, "used" : 0, "price" : 20, "quantity" : 1, "date" : ISODate("2014-02-03T09:00:00Z") },
];
*/
```


<br><br>
____________________________________________________
<br><br>
- $listSessions	Lists all sessions that have been active long enough to propagate to the system.sessions collection. (https://docs.mongodb.com/manual/reference/operator/aggregation/listSessions/#pipe._S_listSessions)





<br><br>
____________________________________________________
<br><br>
- $lookup	Performs a left outer join to another collection in the same database to filter in documents from the “joined” collection for processing. (https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/#pipe._S_lookup)
- Guides:
<br> https://www.youtube.com/watch?v=j7ccC2F1yc0
<br> https://www.youtube.com/watch?v=s1KD_Qt7vY4
- In easy words it will join collections together that you can work cross collection.

<br><br>
- **from** (Specifies the collection in the same database to perform the join with. The from collection cannot be sharded (https://docs.mongodb.com/manual/sharding/). **We can not choose collections from different databases**) - https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/#lookup-join-from

<br><br>

- **localField** (Specifies the field from the documents in the from collection. $lookup performs an equality match on the foreignField to the localField from the input documents. If a document in the from collection does not contain the foreignField, the $lookup treats the value as null for matching purposes.) - https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/#lookup-eq-localfield
<br> In easy words this will be the field from our working collection which we compare later with the joined collection field. Works aswell with arrays.

<br><br>

- **foreignField** (Specifies the field from the documents in the from collection. $lookup performs an equality match on the foreignField to the localField from the input documents. If a document in the from collection does not contain the foreignField, the $lookup treats the value as null for matching purposes.) - https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/#lookup-eq-foreignfield
<br> In easy words this will be the field from our joined collection which we compare later with the working collection field.  Works aswell with arrays.

<br><br>

- **let** (Specifies variables to use in the pipeline field stages. Use the variable expressions to access the fields from the documents input to the $lookup stage.
<br> In other words the pipleline only has access to the current collection where we run the lookup. To get access from the source collection where we run the join we use let to define the fields where we want access) - https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/#lookup-join-let

<br><br>

- **pipeline** (Specifies the pipeline to run on the joined collection. The pipeline determines the resulting documents from the joined collection. To return all documents, specify an empty pipeline [].) - https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/#lookup-join-pipeline

<br><br>

- **as** (Specifies the name of the new array field to add to the input documents. The new array field contains the matching documents from the from collection.) - https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/#lookup-join-as
<br> **If the specified name already exists in the input document, the existing field is overwritten!**
<br> If there is no match there will be an empty array.


<br><br>
- Syntax:
```javascript
// ---- Equality Match ----
{
   $lookup:
     {
       from: <collection to join>,
       localField: <field from the input documents>,
       foreignField: <field from the documents of the "from" collection>,
       as: <output array field>
     }
}

/* The operation would correspond to the following pseudo-SQL statement:
SELECT *, <output array field>
FROM collection
WHERE <output array field> IN (SELECT *
                               FROM <collection to join>
                               WHERE <foreignField>= <collection.localField>);
*/







// ---- Join Conditions and Uncorrelated Sub-queries ----
{
   $lookup:
     {
       from: <collection to join>,
       let: { <var_1>: <expression>, …, <var_n>: <expression> },
       pipeline: [ <pipeline to execute on the collection to join> ],
       as: <output array field>
     }
}

/*
SELECT *, <output array field>
FROM collection
WHERE <output array field> IN (SELECT <documents as determined from the pipeline>
                               FROM <collection to join>
                               WHERE <pipeline> );
*/












// ---- Consideration ----
{
  $lookup:
    {
       from: <collection to join>,
       let: { <var_1>: <expression>, …, <var_n>: <expression> },
       pipeline: [ <pipeline to execute on the joined collection> ],  // Cannot include $out or $merge
       as: <output array field>
    }
}
```


```javascript
// ------ EXAMPLE #1 -------
/* // orders collections
[
   { "_id" : 1, "item" : "almonds", "price" : 12, "quantity" : 2 },
   { "_id" : 2, "item" : "pecans", "price" : 20, "quantity" : 1 },
   { "_id" : 3  }
]
*/


/* // inventory collection
[
   { "_id" : 1, "sku" : "almonds", "description": "product 1", "instock" : 120 },
   { "_id" : 2, "sku" : "bread", "description": "product 2", "instock" : 80 },
   { "_id" : 3, "sku" : "cashews", "description": "product 3", "instock" : 60 },
   { "_id" : 4, "sku" : "pecans", "description": "product 4", "instock" : 70 },
   { "_id" : 5, "sku": null, "description": "Incomplete" },
   { "_id" : 6 }
]
*/

The following aggregation operation on the orders collection joins the documents from orders with the documents from the inventory collection using the fields item from the orders collection and the sku field from the inventory collection:
const pipeline = [
   {
     $lookup:
       {
         from: "inventory",
         localField: "item",
         foreignField: "sku",
         as: "inventory_docs"
       }
  }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
{
   "_id" : 1,
   "item" : "almonds",
   "price" : 12,
   "quantity" : 2,
   "inventory_docs" : [
      { "_id" : 1, "sku" : "almonds", "description" : "product 1", "instock" : 120 }
   ]
}
{
   "_id" : 2,
   "item" : "pecans",
   "price" : 20,
   "quantity" : 1,
   "inventory_docs" : [
      { "_id" : 4, "sku" : "pecans", "description" : "product 4", "instock" : 70 }
   ]
}
{
   "_id" : 3,
   "inventory_docs" : [
      { "_id" : 5, "sku" : null, "description" : "Incomplete" },
      { "_id" : 6 }
   ]
}
*/

/* // The operation would correspond to the following pseudo-SQL statement:
SELECT *, inventory_docs
FROM orders
WHERE inventory_docs IN (SELECT *
FROM inventory
WHERE sku= orders.item);
*/


























// ------ EXAMPLE #2 - Use $lookup with an Array -------
/* // classes collection
[
   { _id: 1, title: "Reading is ...", enrollmentlist: [ "giraffe2", "pandabear", "artie" ], days: ["M", "W", "F"] },
   { _id: 2, title: "But Writing ...", enrollmentlist: [ "giraffe1", "artie" ], days: ["T", "F"] }
]
*/


/* // members collections
[
   { _id: 1, name: "artie", joined: new Date("2016-05-01"), status: "A" },
   { _id: 2, name: "giraffe", joined: new Date("2017-05-01"), status: "D" },
   { _id: 3, name: "giraffe1", joined: new Date("2017-10-01"), status: "A" },
   { _id: 4, name: "panda", joined: new Date("2018-10-11"), status: "A" },
   { _id: 5, name: "pandabear", joined: new Date("2018-12-01"), status: "A" },
   { _id: 6, name: "giraffe2", joined: new Date("2018-12-01"), status: "D" }
]
*/

// The following aggregation operation joins documents in the classes collection with the members collection, matching on the members field to the name field:
const pipeline = [
   {
      $lookup:
         {
            from: "members",
            localField: "enrollmentlist",
            foreignField: "name",
            as: "enrollee_info"
        }
   }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
{
   "_id" : 1,
   "title" : "Reading is ...",
   "enrollmentlist" : [ "giraffe2", "pandabear", "artie" ],
   "days" : [ "M", "W", "F" ],
   "enrollee_info" : [
      { "_id" : 1, "name" : "artie", "joined" : ISODate("2016-05-01T00:00:00Z"), "status" : "A" },
      { "_id" : 5, "name" : "pandabear", "joined" : ISODate("2018-12-01T00:00:00Z"), "status" : "A" },
      { "_id" : 6, "name" : "giraffe2", "joined" : ISODate("2018-12-01T00:00:00Z"), "status" : "D" }
   ]
}
{
   "_id" : 2,
   "title" : "But Writing ...",
   "enrollmentlist" : [ "giraffe1", "artie" ],
   "days" : [ "T", "F" ],
   "enrollee_info" : [
      { "_id" : 1, "name" : "artie", "joined" : ISODate("2016-05-01T00:00:00Z"), "status" : "A" },
      { "_id" : 3, "name" : "giraffe1", "joined" : ISODate("2017-10-01T00:00:00Z"), "status" : "A" }
   ]
}
*/



































// ------ EXAMPLE #3 - Use $lookup with $mergeObjects -------
/* // orders collection
[
   { "_id" : 1, "item" : "almonds", "price" : 12, "quantity" : 2 },
   { "_id" : 2, "item" : "pecans", "price" : 20, "quantity" : 1 }
]
*/


/* // items collections
[
  { "_id" : 1, "item" : "almonds", description: "almond clusters", "instock" : 120 },
  { "_id" : 2, "item" : "bread", description: "raisin and nut bread", "instock" : 80 },
  { "_id" : 3, "item" : "pecans", description: "candied pecans", "instock" : 60 }
]
*/

// The following operation first uses the $lookup stage to join the two collections by the item fields and then uses $mergeObjects in the $replaceRoot to merge the joined documents from items and orders:
const pipeline = [
   {
      $lookup: {
         from: "items",
         localField: "item",    // field in the orders collection
         foreignField: "item",  // field in the items collection
         as: "fromItems"
      }
   },
   {
      $replaceRoot: { newRoot: { $mergeObjects: [ { $arrayElemAt: [ "$fromItems", 0 ] }, "$$ROOT" ] } }
   },
   { $project: { fromItems: 0 } }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
{ "_id" : 1, "item" : "almonds", "description" : "almond clusters", "instock" : 120, "price" : 12, "quantity" : 2 }
{ "_id" : 2, "item" : "pecans", "description" : "candied pecans", "instock" : 60, "price" : 20, "quantity" : 1 }
*/





























// ------ EXAMPLE #4 - Specify Multiple Join Conditions with $lookup -------
/* // orders collection
[
  { "_id" : 1, "item" : "almonds", "price" : 12, "ordered" : 2 },
  { "_id" : 2, "item" : "pecans", "price" : 20, "ordered" : 1 },
  { "_id" : 3, "item" : "cookies", "price" : 10, "ordered" : 60 }
]
*/


/* // warehouses collections
[
  { "_id" : 1, "stock_item" : "almonds", warehouse: "A", "instock" : 120 },
  { "_id" : 2, "stock_item" : "pecans", warehouse: "A", "instock" : 80 },
  { "_id" : 3, "stock_item" : "almonds", warehouse: "B", "instock" : 60 },
  { "_id" : 4, "stock_item" : "cookies", warehouse: "B", "instock" : 40 },
  { "_id" : 5, "stock_item" : "cookies", warehouse: "A", "instock" : 80 }
]
*/

// The following operation joins the orders collection with the warehouse collection by the item and whether the quantity in stock is sufficient to cover the ordered quantity:
const pipeline = [
   {
      $lookup:
         {
           from: "warehouses",
           let: { order_item: "$item", order_qty: "$ordered" },
           pipeline: [
              { $match:
                 { $expr:
                    { $and:
                       [
                         { $eq: [ "$stock_item",  "$$order_item" ] },
                         { $gte: [ "$instock", "$$order_qty" ] }
                       ]
                    }
                 }
              },
              { $project: { stock_item: 0, _id: 0 } }
           ],
           as: "stockdata"
         }
    }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
[
  { "_id" : 1, "item" : "almonds", "price" : 12, "ordered" : 2, "stockdata" : [ { "warehouse" : "A", "instock" : 120 }, { "warehouse" : "B", "instock" : 60 } ] },
  { "_id" : 2, "item" : "pecans", "price" : 20, "ordered" : 1, "stockdata" : [ { "warehouse" : "A", "instock" : 80 } ] },
  { "_id" : 3, "item" : "cookies", "price" : 10, "ordered" : 60, "stockdata" : [ { "warehouse" : "A", "instock" : 80 } ] },
]
*/


/* // The operation corresponds to the following pseudo-SQL statement:
SELECT *, stockdata
FROM orders
WHERE stockdata IN ( SELECT warehouse, instock
                     FROM warehouses
                     WHERE stock_item = orders.item
                     AND instock >= orders.ordered );
*/























// ------ EXAMPLE #5 - Uncorrelated Subquery -------
/* // absenses collection
[
   { "_id" : 1, "student" : "Ann Aardvark", sickdays: [ new Date ("2018-05-01"),new Date ("2018-08-23") ] },
   { "_id" : 2, "student" : "Zoe Zebra", sickdays: [ new Date ("2018-02-01"),new Date ("2018-05-23") ] },
]
*/


/* // holidays collections
[
   { "_id" : 1, year: 2018, name: "New Years", date: new Date("2018-01-01") },
   { "_id" : 2, year: 2018, name: "Pi Day", date: new Date("2018-03-14") },
   { "_id" : 3, year: 2018, name: "Ice Cream Day", date: new Date("2018-07-15") },
   { "_id" : 4, year: 2017, name: "New Years", date: new Date("2017-01-01") },
   { "_id" : 5, year: 2017, name: "Ice Cream Day", date: new Date("2017-07-16") }
]
*/

// The following operation joins the orders collection with the warehouse collection by the item and whether the quantity in stock is sufficient to cover the ordered quantity:
const pipeline = [
   {
      $lookup:
         {
           from: "holidays",
           pipeline: [
              { $match: { year: 2018 } },
              { $project: { _id: 0, date: { name: "$name", date: "$date" } } },
              { $replaceRoot: { newRoot: "$date" } }
           ],
           as: "holidays"
         }
    }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
[
  { "_id" : 1, "student" : "Ann Aardvark", "sickdays" : [ ISODate("2018-05-01T00:00:00Z"), ISODate("2018-08-23T00:00:00Z") ], "holidays" : [ { "name" : "New Years", "date" : ISODate("2018-01-01T00:00:00Z") }, { "name" : "Pi Day", "date" : ISODate("2018-03-14T00:00:00Z") }, { "name" : "Ice Cream Day", "date" : ISODate("2018-07-15T00:00:00Z") } ] },
  { "_id" : 2, "student" : "Zoe Zebra", "sickdays" : [ ISODate("2018-02-01T00:00:00Z"), ISODate("2018-05-23T00:00:00Z") ], "holidays" : [ { "name" : "New Years", "date" : ISODate("2018-01-01T00:00:00Z") }, { "name" : "Pi Day", "date" : ISODate("2018-03-14T00:00:00Z") }, { "name" : "Ice Cream Day", "date" : ISODate("2018-07-15T00:00:00Z") } ] },
]
*/


/* // The operation corresponds to the following pseudo-SQL statement:
SELECT *, holidays
FROM absences
WHERE holidays IN (SELECT name, date
                    FROM holidays
                    WHERE year = 2018);
*/

```


<br><br>
____________________________________________________
<br><br>
- $match	Filters the document stream to allow only matching documents to pass unmodified into the next pipeline stage. For each input document, outputs either one document (a match) or zero documents (no match). (https://docs.mongodb.com/manual/reference/operator/aggregation/match/#pipe._S_match)
- $match uses standard MongoDB Query Operators.
- We can not use $where
- If we use $text the $match stage must be the first.
- If $match is first stage it can take advantages of index and is faster.
- $match uses the same query syntax as find and you can compare it to filter from javascript.





<br><br>
____________________________________________________
<br><br>
- $merge	Writes the resulting documents of the aggregation pipeline to a collection. The stage can incorporate (insert new documents, merge documents, replace documents, keep existing documents, fail the operation, process documents with a custom update pipeline) the results into an output collection.
<br><br>
**To use the $merge stage, it must be the last stage in the pipeline.** (https://docs.mongodb.com/manual/reference/operator/aggregation/merge/#pipe._S_merge)
- Guides:
<br> https://www.youtube.com/watch?v=dz2dBL_5Lrg

<br><br>
- Syntax:
```javascript
{ $merge: {
     into: <collection> -or- { db: <db>, coll: <collection> },
     on: <identifier field> -or- [ <identifier field1>, ...],  // Optional
     let: <variables>,                                         // Optional
     whenMatched: <replace|keepExisting|merge|fail|pipeline>,  // Optional
     whenNotMatched: <insert|discard|fail>                     // Optional
} }
```
- Options:
```javascript
into | The output collection. Specify either:
- The collection name as a string to output to a collection in the same database where the aggregation is run. For example:
-- into: "myOutput"

The database and collection name in a document to output to a collection in the specified database. For example:
- into: { db:"myDB", coll:"myOutput" }




on	| Optional. Field or fields that act as a unique identifier for a document. The identifier determines if a results document matches an already existing document in the output collection. Specify either:
- A single field name as a string. For example:
-- on: "_id"

A combination of fields in an array. For example:
- on: [ "date", "customerId" ]
- The order of the fields in the array does not matter, and you cannot specify the same field multiple times.




whenMatched	| Optional. The behavior of $merge if a result document and an existing document in the collection have the same value for the specified on field(s).

let	| Optional. Specifies variables accessible for use in the whenMatched pipeline

whenNotMatched	| Optional. The behavior of $merge if a result document does not match an existing document in the out collection.
```
- Example:
```javascript
const pipeline = [
    { $merge: { into: "myOutput", on: "_id", whenMatched: "replace", whenNotMatched: "insert" } }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});
```




<br><br>
____________________________________________________
<br><br>
- $out	Writes the resulting documents of the aggregation pipeline to a collection. **To use the $out stage, it must be the last stage in the pipeline. Also the collection must not exist, if it does exist it will get overwritten. When you create a new collection you must always have unique _id our you get a error.**. (https://docs.mongodb.com/manual/reference/operator/aggregation/out/#pipe._S_out)
- Guides:
<br> https://www.youtube.com/watch?v=jC4oMA0riWo

<br><br>
- **No use withing $facet**
<br><br>

- Syntax:
```javascript
{ $out: { db: "<output-db>", coll: "<output-collection>" } }
```
- Options:
```javascript
db	| The output database name.
- For a replica set or a standalone, if the output database does not exist, $out also creates the database.
- For a sharded cluster, the specified output database must already exist.

coll | The output collection name.
```
- Example:
```javascript
// ---- EXAMPLE #1 - Output to Same Database ----

/* Our collection looks like this:
[
   { "_id" : 8751, "title" : "The Banquet", "author" : "Dante", "copies" : 2 },
   { "_id" : 8752, "title" : "Divine Comedy", "author" : "Dante", "copies" : 1 },
   { "_id" : 8645, "title" : "Eclogues", "author" : "Dante", "copies" : 2 },
   { "_id" : 7000, "title" : "The Odyssey", "author" : "Homer", "copies" : 10 },
   { "_id" : 7020, "title" : "Iliad", "author" : "Homer", "copies" : 10 }
]
*/

// The following aggregation operation pivots the data in the books collection in the test database to have titles grouped by authors and then writes the results to the authors collection, also in the test database.
const pipeline = [
    { $group : { _id : "$author", books: { $push: "$title" } } },
    { $out : "authors" }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // The $group stage groups by the authors and uses $push to add the titles to a books array field:
{ "_id" : "Dante", "books" : [ "The Banquet", "Divine Comedy", "Eclogues" ] }
{ "_id" : "Homer", "books" : [ "The Odyssey", "Iliad" ] }


Second Stage ($out):
The $out stage outputs the documents to the authors collection in the test database.
To view the documents in the output collection, run the following operation:

db.getSiblingDB("test").authors.find()
*/

/* // result:
[
  { "_id" : "Homer", "books" : [ "The Odyssey", "Iliad" ] },
  { "_id" : "Dante", "books" : [ "The Banquet", "Divine Comedy", "Eclogues" ] },
]
*/






























// ---- EXAMPLE #2 - Output to Same Database ----

/* Our collection looks like this:
[
   { "_id" : 8751, "title" : "The Banquet", "author" : "Dante", "copies" : 2 },
   { "_id" : 8752, "title" : "Divine Comedy", "author" : "Dante", "copies" : 1 },
   { "_id" : 8645, "title" : "Eclogues", "author" : "Dante", "copies" : 2 },
   { "_id" : 7000, "title" : "The Odyssey", "author" : "Homer", "copies" : 10 },
   { "_id" : 7020, "title" : "Iliad", "author" : "Homer", "copies" : 10 }
]
*/

// The following aggregation operation pivots the data in the books collection to have titles grouped by authors and then writes the results to the authors collection in the reporting database:
const pipeline = [
    { $group : { _id : "$author", books: { $push: "$title" } } },
    { $out : { db: "reporting", coll: "authors" } }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* 

First Stage ($group):
The $group stage groups by the authors and uses $push to add the titles to a books array field:

{ "_id" : "Dante", "books" : [ "The Banquet", "Divine Comedy", "Eclogues" ] }
{ "_id" : "Homer", "books" : [ "The Odyssey", "Iliad" ] }


Second Stage ($out):
The $out stage outputs the documents to the authors collection in the reporting database.
To view the documents in the output collection, run the following operation:

db.getSiblingDB("reporting").authors.find()
*/

/* // result:
[
  { "_id" : "Homer", "books" : [ "The Odyssey", "Iliad" ] },
  { "_id" : "Dante", "books" : [ "The Banquet", "Divine Comedy", "Eclogues" ] },
]
*/
```

<br><br>
____________________________________________________
<br><br>
- $planCacheStats	Returns plan cache information for a collection. (https://docs.mongodb.com/manual/reference/operator/aggregation/planCacheStats/#pipe._S_planCacheStats)




<br><br>
____________________________________________________
<br><br>
- **$project**	Reshapes each document in the stream, such as by adding new fields or removing existing fields. For each input document, outputs one document. See also $unset for removing existing fields. (https://docs.mongodb.com/manual/reference/operator/aggregation/project/#pipe._S_project)
- You must manually specify each field which you want to return. Only **_id** field will be also returned! If you do not want this then use **{_id: 0}**
- You can compare it with .map from javascript.
- Can be used as many time as you want within aggregation pipeline.
- Accumulator Expressions only works with an array inside of our current document. They do not carry values over all documents.
- Avaible Accumulator Expressions are: $sum, $avg, $max, $min, $stdDevPop, $stdDevSam
```javascript
const pipeline = [{$project: {_id: 0, item: 1}}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});
```




<br><br>
____________________________________________________
<br><br>
- $redact	Reshapes each document in the stream by restricting the content for each document based on information stored in the documents themselves. Incorporates the functionality of $project and $match. Can be used to implement field level redaction. For each input document, outputs either one or zero documents. (https://docs.mongodb.com/manual/reference/operator/aggregation/redact/#pipe._S_redact)
- In easy words you can search nested objects for the same fields and check for a specific value.

<br><br>
- Syntax:
```javascript
{ $redact: <expression> }
```
- System Variable:
```javascript
/*
$$DESCEND	$redact returns the fields at the current document level, excluding embedded documents. To include embedded documents and embedded documents within arrays, apply the $cond expression to the embedded documents to determine access for these embedded documents.

$$PRUNE	$redact excludes all fields at this current document/embedded document level, without further inspection of any of the excluded fields. This applies even if the excluded field contains embedded documents that may have different access levels.

$$KEEP	$redact returns or keeps all fields at this current document/embedded document level, without further inspection of the fields at this level. This applies even if the included field contains embedded documents that may have different access levels.
*/
```
- Example:
```javascript
// ---- EXAMPLE #1  - Evaluate Access at Every Document Level ----

/* Our collection looks like this:
{
  _id: 1,
  title: "123 Department Report",
  tags: [ "G", "STLW" ],
  year: 2014,
  subsections: [
    {
      subtitle: "Section 1: Overview",
      tags: [ "SI", "G" ],
      content:  "Section 1: This is the content of section 1."
    },
    {
      subtitle: "Section 2: Analysis",
      tags: [ "STLW" ],
      content: "Section 2: This is the content of section 2."
    },
    {
      subtitle: "Section 3: Budgeting",
      tags: [ "TK" ],
      content: {
        text: "Section 3: This is the content of section3.",
        tags: [ "HCS" ]
      }
    }
  ]
}
*/

// A user has access to view information with either the tag "STLW" or "G". To run a query on all documents with year 2014 for this user, include a $redact stage as in the following:
const userAccess = [ "STLW", "G" ];
const pipeline = [
     { $match: { year: 2014 } },
     { $redact: {
        $cond: {
           if: { $gt: [ { $size: { $setIntersection: [ "$tags", userAccess ] } }, 0 ] },
           then: "$$DESCEND",
           else: "$$PRUNE"
         }
       }
     }
   ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
{
  "_id" : 1,
  "title" : "123 Department Report",
  "tags" : [ "G", "STLW" ],
  "year" : 2014,
  "subsections" : [
    {
      "subtitle" : "Section 1: Overview",
      "tags" : [ "SI", "G" ],
      "content" : "Section 1: This is the content of section 1."
    },
    {
      "subtitle" : "Section 2: Analysis",
      "tags" : [ "STLW" ],
      "content" : "Section 2: This is the content of section 2."
    }
  ]
}
*/

































// ---- EXAMPLE #2  - Exclude All Fields at a Given Level ----

/* Our collection looks like this:
{
  _id: 1,
  level: 1,
  acct_id: "xyz123",
  cc: {
    level: 5,
    type: "yy",
    num: 000000000000,
    exp_date: ISODate("2015-11-01T00:00:00.000Z"),
    billing_addr: {
      level: 5,
      addr1: "123 ABC Street",
      city: "Some City"
    },
    shipping_addr: [
      {
        level: 3,
        addr1: "987 XYZ Ave",
        city: "Some City"
      },
      {
        level: 3,
        addr1: "PO Box 0123",
        city: "Some City"
      }
    ]
  },
  status: "A"
}
*/

// To run a query on all documents with status A and exclude all fields contained in a document/embedded document at level 5, include a $redact stage that specifies the system variable "$$PRUNE" in the then field:
const pipeline = [
    { $match: { status: "A" } },
    {
      $redact: {
        $cond: {
          if: { $eq: [ "$level", 5 ] },
          then: "$$PRUNE",
          else: "$$DESCEND"
        }
      }
    }
  ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
{
  "_id" : 1,
  "level" : 1,
  "acct_id" : "xyz123",
  "status" : "A"
}
*/
```





<br><br>
____________________________________________________
<br><br>
- $replaceRoot	Replaces a document with the specified embedded document. The operation replaces all existing fields in the input document, including the _id field. Specify a document embedded in the input document to promote the embedded document to the top level. (https://docs.mongodb.com/manual/reference/operator/aggregation/replaceRoot/#pipe._S_replaceRoot)
- Syntax:
```javascript
{$sample: { size: <positive integer> }}
```
```javascript
/* // source collection
[
  { "_id" : 1, "name" : "Arlene", "age" : 34, "pets" : { "dogs" : 2, "cats" : 1 } },
  { "_id" : 2, "name" : "Sam", "age" : 41, "pets" : { "cats" : 1, "fish" : 3 } },
  { "_id" : 3, "name" : "Maria", "age" : 25 },
]
*/

// The following operation uses the $replaceRoot stage to replace each input document with the result of a $mergeObjects operation. The $mergeObjects expression merges the specified default document with the pets document.
const pipeline = [
   { $replaceRoot: { newRoot: { $mergeObjects:  [ { dogs: 0, cats: 0, birds: 0, fish: 0 }, "$pets" ] }} }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
[
  { "dogs" : 2, "cats" : 1, "birds" : 0, "fish" : 0 },
  { "dogs" : 0, "cats" : 1, "birds" : 0, "fish" : 3 },
  { "dogs" : 0, "cats" : 0, "birds" : 0, "fish" : 0 },
]
*/
```



<br><br>
____________________________________________________
<br><br>
- $replaceWith is an alias for $replaceRoot stage. Replaces a document with the specified embedded document. The operation replaces all existing fields in the input document, including the _id field. Specify a document embedded in the input document to promote the embedded document to the top level. $replaceWith is an alias for $replaceRoot stage. (https://docs.mongodb.com/manual/reference/operator/aggregation/replaceWith/)
 
<br><br>
- Syntax:
```javascript
{ $replaceWith: <replacementDocument> }
```
- Example:
```javascript
// ---- EXAMPLE #1 - $replaceWith an Embedded Document Field ----

/* source collection:
[
   { "_id" : 1, "name" : "Arlene", "age" : 34, "pets" : { "dogs" : 2, "cats" : 1 } },
   { "_id" : 2, "name" : "Sam", "age" : 41, "pets" : { "cats" : 1, "fish" : 3 } },
   { "_id" : 3, "name" : "Maria", "age" : 25 }
]
*/

// The following operation uses the $replaceWith stage to replace each input document with the result of a $mergeObjects operation. The $mergeObjects expression merges the specified default document with the pets document.
const pipeline = [
   { $replaceWith: { $mergeObjects:  [ { dogs: 0, cats: 0, birds: 0, fish: 0 }, "$pets" ] } }
];


// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
[
  { "dogs" : 2, "cats" : 1, "birds" : 0, "fish" : 0 },
  { "dogs" : 0, "cats" : 1, "birds" : 0, "fish" : 3 },
  { "dogs" : 0, "cats" : 0, "birds" : 0, "fish" : 0 },
]
*/







































// ---- EXAMPLE #2 - $replaceWith a Document Nested in an Array ----

/* source collection:
[
   {
      "_id" : 1,
      "grades" : [
         { "test": 1, "grade" : 80, "mean" : 75, "std" : 6 },
         { "test": 2, "grade" : 85, "mean" : 90, "std" : 4 },
         { "test": 3, "grade" : 95, "mean" : 85, "std" : 6 }
      ]
   },
   {
      "_id" : 2,
      "grades" : [
         { "test": 1, "grade" : 90, "mean" : 75, "std" : 6 },
         { "test": 2, "grade" : 87, "mean" : 90, "std" : 3 },
         { "test": 3, "grade" : 91, "mean" : 85, "std" : 4 }
      ]
   }
]
*/

// The following operation uses the $replaceWith stage to replace each input document with the result of a $mergeObjects operation. The $mergeObjects expression merges the specified default document with the pets document.
const pipeline = [
   { $unwind: "$grades" },
   { $match: { "grades.grade" : { $gte: 90 } } },
   { $replaceWith: "$grades" }
];


// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
[
  { "test" : 3, "grade" : 95, "mean" : 85, "std" : 6 },
  { "test" : 1, "grade" : 90, "mean" : 75, "std" : 6 },
  { "test" : 3, "grade" : 91, "mean" : 85, "std" : 4 },
]
*/








































// ---- EXAMPLE #3 - $replaceWith a Newly Created Document ----

/* source collection:
[
   { "_id" : 1, "item" : "butter", "price" : 10, "quantity": 2, date: ISODate("2019-03-01T08:00:00Z"), status: "C" },
   { "_id" : 2, "item" : "cream", "price" : 20, "quantity": 1, date: ISODate("2019-03-01T09:00:00Z"), status: "A" },
   { "_id" : 3, "item" : "jam", "price" : 5, "quantity": 10, date: ISODate("2019-03-15T09:00:00Z"), status: "C" },
   { "_id" : 4, "item" : "muffins", "price" : 5, "quantity": 10, date: ISODate("2019-03-15T09:00:00Z"), status: "C" }
]
*/

// The following operation uses the $replaceWith stage to replace each input document with the result of a $mergeObjects operation. The $mergeObjects expression merges the specified default document with the pets document.
const pipeline = [
   { $match: { status: "C" } },
   { $replaceWith: { _id: "$_id", item: "$item", amount: { $multiply: [ "$price", "$quantity"]}, status: "Complete", asofDate: "$$NOW" } }
];


// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
[
  { "_id" : 1, "item" : "butter", "amount" : 20, "status" : "Complete", "asofDate" : ISODate("2019-06-03T22:47:54.812Z") },
  { "_id" : 3, "item" : "jam", "amount" : 50, "status" : "Complete", "asofDate" : ISODate("2019-06-03T22:47:54.812Z") },
  { "_id" : 4, "item" : "muffins", "amount" : 50, "status" : "Complete", "asofDate" : ISODate("2019-06-03T22:47:54.812Z") },
]
*/

















































// ---- EXAMPLE #3 (b) - $replaceWith a Newly Created Document ----

/* source collection:
[
   { _id: 1, quarter: "2019Q1", region: "A", qty: 400 },
   { _id: 2, quarter: "2019Q1", region: "B", qty: 550 },
   { _id: 3, quarter: "2019Q1", region: "C", qty: 1000 },
   { _id: 4, quarter: "2019Q2", region: "A", qty: 660 },
   { _id: 5, quarter: "2019Q2", region: "B", qty: 500 },
   { _id: 6, quarter: "2019Q2", region: "C", qty: 1200 }
]
*/

// The following operation uses the $replaceWith stage to replace each input document with the result of a $mergeObjects operation. The $mergeObjects expression merges the specified default document with the pets document.
const pipeline = [
   { $addFields: { obj:  { k: "$region", v: "$qty" } } },
   { $group: { _id: "$quarter", items: { $push: "$obj" } } },
   { $project: { items2: { $concatArrays: [ [ { "k": "_id", "v": "$_id" } ], "$items" ] } } },
   { $replaceWith: { $arrayToObject: "$items2" } }
];


// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
[
  { "_id" : "2019Q1", "A" : 400, "B" : 550, "C" : 1000 }
  { "_id" : "2019Q2", "A" : 660, "B" : 500, "C" : 1200 }
]
*/


















































// ---- EXAMPLE #4 - $replaceWith a New Document Created from $$ROOT and a Default Document ----

/* source collection:
[
   { "_id" : 1, name: "Fred", email: "fred@example.net" },
   { "_id" : 2, name: "Frank N. Stine", cell: "012-345-9999" },
   { "_id" : 3, name: "Gren Dell", cell: "987-654-3210", email: "beo@example.net" }
]
*/

// The following operation uses the $replaceWith stage to replace each input document with the result of a $mergeObjects operation. The $mergeObjects expression merges the specified default document with the pets document.
const pipeline = [
   { $replaceWith: { $mergeObjects: [ { _id: "", name: "", email: "", cell: "", home: "" }, "$$ROOT" ] } }
];


// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
[
  { "_id" : 1, "name" : "Fred", "email" : "fred@example.net", "cell" : "", "home" : "" },
  { "_id" : 2, "name" : "Frank N. Stine", "email" : "", "cell" : "012-345-9999", "home" : "" },
  { "_id" : 3, "name" : "Gren Dell", "email" : "beo@example.net", "cell" : "", "home" : "987-654-3210" },
]
*/
```




<br><br>
____________________________________________________
<br><br>
- $sample	Randomly selects the specified number of documents from its input. (https://docs.mongodb.com/manual/reference/operator/aggregation/sample/#pipe._S_sample)


<br><br>
____________________________________________________
<br><br>
- $sample uses one of two methods to obtain N random documents, depending on the size of the collection, the size of N, and $sample’s position in the pipeline. If all the following conditions are met, $sample uses a pseudo-random cursor to select documents:
<br>$sample is the first stage of the pipeline
<br>N is less than 5% of the total documents in the collection
<br>The collection contains more than 100 documents
- Syntax:
```javascript
{$sample: { size: <positive integer> }}
```
```javascript
/* // source collection
[
  { "_id" : 1, "name" : "dave123", "q1" : true, "q2" : true },
  { "_id" : 2, "name" : "dave2", "q1" : false, "q2" : false  },
  { "_id" : 3, "name" : "ahn", "q1" : true, "q2" : true  },
  { "_id" : 4, "name" : "li", "q1" : true, "q2" : false  },
  { "_id" : 5, "name" : "annT", "q1" : false, "q2" : true  },
  { "_id" : 6, "name" : "li", "q1" : true, "q2" : true  },
  { "_id" : 7, "name" : "ty", "q1" : false, "q2" : true  },
]
*/

const pipeline = [{$sample: {size: 3}}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
[
  { "_id" : 3, "name" : "ahn", "q1" : true, "q2" : true  },
  { "_id" : 4, "name" : "li", "q1" : true, "q2" : false  },
  { "_id" : 7, "name" : "ty", "q1" : false, "q2" : true  },
]
*/
```


<br><br>
____________________________________________________
<br><br>
- $set	Adds new fields to documents. Similar to $project, $set reshapes each document in the stream; specifically, by adding new fields to output documents that contain both the existing fields from the input documents and the newly added fields.


<br><br>
____________________________________________________
<br><br>
- $set is an alias for $addFields stage. (https://docs.mongodb.com/manual/reference/operator/aggregation/set/#pipe._S_set)



<br><br>
____________________________________________________
<br><br>
- $skip	Skips the first n documents where n is the specified skip number and passes the remaining documents unmodified to the pipeline. For each input document, outputs either zero documents (for the first n documents) or one document (if after the first n documents). (https://docs.mongodb.com/manual/reference/operator/aggregation/skip/#pipe._S_skip)
- Syntax:
```javascript
{ $skip: <positive integer> }
```
- Example
```javascript
/* // source collection:
[
  {_id: '1', title: 'Fortnitev1'},
  {_id: '2', title: 'Fortnitev2'},
  {_id: '3', title: 'Fortnitev3'},
  {_id: '4', title: 'Fortnitev4'},
  {_id: '5', title: 'Fortnitev5'},
]
*/

// skip first 2 documents in natural order
const pipeline = [{$skip: 2}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
[
  {_id: '3', title: 'Fortnitev3'},
  {_id: '4', title: 'Fortnitev4'},
  {_id: '5', title: 'Fortnitev5'},
]
*/
```



<br><br>
____________________________________________________
<br><br>
- $sort	Reorders the document stream by a specified sort key. Only the order changes; the documents remain unmodified. For each input document, outputs one document. (https://docs.mongodb.com/manual/reference/operator/aggregation/sort/#pipe._S_sort)
- You can sort on multiple fields. The sort priority will be in order of your sort queries.
- Can take advantage of indexes if used earlier in the pipeline.
- By default $sort will only use 100MB of RAM. To increase the limit use allowDiskUse.
- Syntax:
```javascript
{ $sort: { <field1>: <sort order>, <field2>: <sort order> ... } }
```
- Options:
```javascript
1	| Sort ascending.
-1 | Sort descending.
{$meta: "textScore"} | Sort by the computed textScore metadata in descending order. See Text Score Metadata Sort for an example.
```
- Example
```javascript
// ------ SINGLE SORT --------
/* // source collection:
[
   { "_id" : 1, "name" : "Central Park Cafe", "borough" : "Manhattan"},
   { "_id" : 2, "name" : "Rock A Feller Bar and Grill", "borough" : "Queens"},
   { "_id" : 3, "name" : "Empire State Pub", "borough" : "Brooklyn"},
   { "_id" : 4, "name" : "Stan's Pizzaria", "borough" : "Manhattan"},
   { "_id" : 5, "name" : "Jane's Deli", "borough" : "Brooklyn"},
]
*/

// sort the borough field is ascending order
const pipeline = [
     { $sort : { borough : 1 } }
   ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:

{ "_id" : 3, "name" : "Empire State Pub", "borough" : "Brooklyn" }
{ "_id" : 5, "name" : "Jane's Deli", "borough" : "Brooklyn" }
{ "_id" : 1, "name" : "Central Park Cafe", "borough" : "Manhattan" }
{ "_id" : 4, "name" : "Stan's Pizzaria", "borough" : "Manhattan" }
{ "_id" : 2, "name" : "Rock A Feller Bar and Grill", "borough" : "Queens" }
*/











// ------ MULTIPLE SORT --------
/* // source collection:
[
   { "_id" : 1, "name" : "Central Park Cafe", "borough" : "Manhattan"},
   { "_id" : 2, "name" : "Rock A Feller Bar and Grill", "borough" : "Queens"},
   { "_id" : 3, "name" : "Empire State Pub", "borough" : "Brooklyn"},
   { "_id" : 4, "name" : "Stan's Pizzaria", "borough" : "Manhattan"},
   { "_id" : 5, "name" : "Jane's Deli", "borough" : "Brooklyn"},
]
*/

// First sort through borough in ascending order and after this sort name in descending order
const pipeline = [
     {$sort : {borough : 1, name: -1}}
   ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
{ "_id" : 5, "name" : "Jane's Deli", "borough" : "Brooklyn" }
{ "_id" : 3, "name" : "Empire State Pub", "borough" : "Brooklyn" }
{ "_id" : 4, "name" : "Stan's Pizzaria", "borough" : "Manhattan" }
{ "_id" : 1, "name" : "Central Park Cafe", "borough" : "Manhattan" }
{ "_id" : 2, "name" : "Rock A Feller Bar and Grill", "borough" : "Queens" }
*/
```


<br><br>
____________________________________________________
<br><br>
- **$sortByCount** - Groups incoming documents based on the value of a specified expression, then computes the count of documents in each distinct group. (https://docs.mongodb.com/manual/reference/operator/aggregation/sortByCount/#pipe._S_sortByCount)
- Syntax:
```javascript
{ $sortByCount:  <expression> }
```
- The $sortByCount stage is equivalent to the following $group + $sort sequence:
```javascript
{ $group: { _id: <expression>, count: { $sum: 1 } } },
{ $sort: { count: -1 } }
```
- Example
```javascript
/* // source collection:
[
  { "_id" : 1, "title" : "The Pillars of Society", "artist" : "Grosz", "year" : 1926, "tags" : [ "painting", "satire", "Expressionism", "caricature" ] },
  { "_id" : 2, "title" : "Melancholy III", "artist" : "Munch", "year" : 1902, "tags" : [ "woodcut", "Expressionism" ] },
  { "_id" : 3, "title" : "Dancer", "artist" : "Miro", "year" : 1925, "tags" : [ "oil", "Surrealism", "painting" ] },
  { "_id" : 4, "title" : "The Great Wave off Kanagawa", "artist" : "Hokusai", "tags" : [ "woodblock", "ukiyo-e" ] },
  { "_id" : 5, "title" : "The Persistence of Memory", "artist" : "Dali", "year" : 1931, "tags" : [ "Surrealism", "painting", "oil" ] },
  { "_id" : 6, "title" : "Composition VII", "artist" : "Kandinsky", "year" : 1913, "tags" : [ "oil", "painting", "abstract" ] },
  { "_id" : 7, "title" : "The Scream", "artist" : "Munch", "year" : 1893, "tags" : [ "Expressionism", "painting", "oil" ] },
  { "_id" : 8, "title" : "Blue Flower", "artist" : "O'Keefe", "year" : 1918, "tags" : [ "abstract", "painting" ] },
]
*/

// The following operation unwinds the tags array and uses the $sortByCount stage to count the number of documents associated with each tag:
const pipeline = [{$unwind: "$tags"},  {$sortByCount: "$tags"}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
[
  { "_id" : "painting", "count" : 6 },
  { "_id" : "oil", "count" : 4 },
  { "_id" : "Expressionism", "count" : 3 },
  { "_id" : "Surrealism", "count" : 2 },
  { "_id" : "abstract", "count" : 2 },
  { "_id" : "woodblock", "count" : 1 },
  { "_id" : "woodcut", "count" : 1 },
  { "_id" : "ukiyo-e", "count" : 1 },
  { "_id" : "satire", "count" : 1 },
  { "_id" : "caricature", "count" : 1 },
]
*/
```



<br><br>
____________________________________________________
<br><br>
- $unionWith	Performs a union of two collections; i.e. combines pipeline results from two collections into a single result set. (https://docs.mongodb.com/manual/reference/operator/aggregation/unionWith/#pipe._S_unionWith)


<br><br>
____________________________________________________
<br><br>
- $unset	Removes/excludes fields from documents. $unset is an alias for $project stage that removes fields.(https://docs.mongodb.com/manual/reference/operator/aggregation/unset/#pipe._S_unset)




<br><br>
____________________________________________________
<br><br>
- $unwind	Deconstructs an array field from the input documents to output a document for each element. Each output document replaces the array with an element value. For each input document, outputs n documents where n is the number of array elements and can be zero for an empty array. (https://docs.mongodb.com/manual/reference/operator/aggregation/unwind/#pipe._S_unwind)
- In easy words it takes each element of an array and create new documents with single fields for each of the array elements.
- **Using $unwind onlarge collections with big documents may lead to performance issues.**
- Syntax:
```javascript
{ $unwind: <field path> }

// another example
{
  $unwind:
    {
      path: <field path>,
      includeArrayIndex: <string>,
      preserveNullAndEmptyArrays: <boolean>
    }
}
```
- Example
```javascript
/* our collection looks like this:
{ "_id" : 1, "item" : "ABC1", sizes: [ "S", "M", "L"] }
*/

// multiply price with quantitiy
const pipeline = [{$unwind : "$sizes"}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
The operation returns the following results:
[
  { "_id" : 1, "item" : "ABC1", "sizes" : "S" },
  { "_id" : 1, "item" : "ABC1", "sizes" : "M" },
  { "_id" : 1, "item" : "ABC1", "sizes" : "L" },
]
*/





// ---- EXAMPLE #2 includeArrayIndex - In easy words with include the index position from the array element which was splitted by $unwind ----
// The following $unwind operation uses the includeArrayIndex option to include the array index in the output.
const pipeline = [
  {
    $unwind:
      {
        path: "$sizes",
        includeArrayIndex: "arrayIndex"
      }
   }];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
The operation returns the following results:
[
  { "_id" : 1, "item" : "ABC", "price" : NumberDecimal("80"), "sizes" : "S", "arrayIndex" : NumberLong(0) },
  { "_id" : 1, "item" : "ABC", "price" : NumberDecimal("80"), "sizes" : "M", "arrayIndex" : NumberLong(1) },
  { "_id" : 1, "item" : "ABC", "price" : NumberDecimal("80"), "sizes" : "L", "arrayIndex" : NumberLong(2) },
  { "_id" : 3, "item" : "IJK", "price" : NumberDecimal("160"), "sizes" : "M", "arrayIndex" : null },
]
*/









// ---- EXAMPLE #3 preserveNullAndEmptyArrays ----

// The following $unwind operation uses the preserveNullAndEmptyArrays option to include documents whose sizes field is null, missing, or an empty array.
const pipeline = [
   { $unwind: { path: "$sizes", preserveNullAndEmptyArrays: true } }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
The output includes those documents where the sizes field is null, missing, or an empty array:
[
  { "_id" : 1, "item" : "ABC", "price" : NumberDecimal("80"), "sizes" : "S" },
  { "_id" : 1, "item" : "ABC", "price" : NumberDecimal("80"), "sizes" : "M" },
  { "_id" : 1, "item" : "ABC", "price" : NumberDecimal("80"), "sizes" : "L" },
  { "_id" : 2, "item" : "EFG", "price" : NumberDecimal("120") },
  { "_id" : 3, "item" : "IJK", "price" : NumberDecimal("160"), "sizes" : "M" },
  { "_id" : 4, "item" : "LMN", "price" : NumberDecimal("10") },
  { "_id" : 5, "item" : "XYZ", "price" : NumberDecimal("5.75"), "sizes" : null },
]
*/
```
<br><br>


















<br><br>
____________________________________________________
____________________________________________________
<br><br>











#### Alphabetical Listing of Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#alphabetical-listing-of-expression-operators)

<br><br>
<br><br>

#### Arithmetic Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#arithmetic-expression-operators)
- $abs	Returns the absolute value of a number. (https://docs.mongodb.com/manual/reference/operator/aggregation/abs/#exp._S_abs)



<br><br>
____________________________________________________
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
____________________________________________________
<br><br>
- $ceil	Returns the smallest integer greater than or equal to the specified number. (https://docs.mongodb.com/manual/reference/operator/aggregation/ceil/#exp._S_ceil)



<br><br>
____________________________________________________
<br><br>
- $divide	Returns the result of dividing the first number by the second. Accepts two argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/divide/#exp._S_divide)
- Syntax:
```javascript
{ $divide: [ <expression1>, <expression2> ] }
```
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
____________________________________________________
<br><br>
- $exp	Raises e to the specified exponent. (https://docs.mongodb.com/manual/reference/operator/aggregation/exp/#exp._S_exp)


<br><br>
____________________________________________________
<br><br>
- $floor	Returns the largest integer less than or equal to the specified number. (https://docs.mongodb.com/manual/reference/operator/aggregation/floor/#exp._S_floor)


<br><br>
____________________________________________________
<br><br>
- $ln	Calculates the natural log of a number. (https://docs.mongodb.com/manual/reference/operator/aggregation/ln/#exp._S_ln)


<br><br>
____________________________________________________
<br><br>
- $log	Calculates the log of a number in the specified base. (https://docs.mongodb.com/manual/reference/operator/aggregation/log/#exp._S_log)


<br><br>
____________________________________________________
<br><br>
- $log10	Calculates the log base 10 of a number. (https://docs.mongodb.com/manual/reference/operator/aggregation/log10/#exp._S_log10)


<br><br>
____________________________________________________
<br><br>
- $mod	Returns the remainder of the first number divided by the second. Accepts two argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/mod/#exp._S_mod)



<br><br>
____________________________________________________
<br><br>
- $multiply	Multiplies numbers to return the product. Accepts any number of argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/multiply/#exp._S_multiply)
- Syntax:
```javascript
{ $multiply: [ <expression1>, <expression2>, ... ] }
```
```javascript
/* our collection looks like this:
{ "_id" : 1, "item" : "abc", "price" : 10, "quantity": 2, date: ISODate("2014-03-01T08:00:00Z") }
{ "_id" : 2, "item" : "jkl", "price" : 20, "quantity": 1, date: ISODate("2014-03-01T09:00:00Z") }
{ "_id" : 3, "item" : "xyz", "price" : 5, "quantity": 10, date: ISODate("2014-03-15T09:00:00Z") }
*/

// multiply price with quantitiy
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
____________________________________________________
<br><br>
- $pow	Raises a number to the specified exponent. (https://docs.mongodb.com/manual/reference/operator/aggregation/pow/#exp._S_pow)


<br><br>
____________________________________________________
<br><br>
- $round	Rounds a number to to a whole integer or to a specified decimal place. (https://docs.mongodb.com/manual/reference/operator/aggregation/round/#exp._S_round)


<br><br>
____________________________________________________
<br><br>
- $sqrt	Calculates the square root. (https://docs.mongodb.com/manual/reference/operator/aggregation/sqrt/#exp._S_sqrt)


<br><br>
____________________________________________________
<br><br>
- $subtract	Returns the result of subtracting the second value from the first. If the two values are numbers, return the difference. If the two values are dates, return the difference in milliseconds. If the two values are a date and a number in milliseconds, return the resulting date. Accepts two argument expressions. If the two values are a date and a number, specify the date argument first as it is not meaningful to subtract a date from a number. (https://docs.mongodb.com/manual/reference/operator/aggregation/subtract/#exp._S_subtract)


<br><br>
____________________________________________________
<br><br>
- $trunc	Truncates a number to a whole integer or to a specified decimal place. (https://docs.mongodb.com/manual/reference/operator/aggregation/trunc/#exp._S_trunc)















<br><br>
____________________________________________________
____________________________________________________
<br><br>









#### Array Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#array-expression-operators)
- $arrayElemAt	Returns the element at the specified array index. (https://docs.mongodb.com/manual/reference/operator/aggregation/arrayElemAt/#exp._S_arrayElemAt)
- Syntax:
```javascript
{ $arrayElemAt: [ <array>, <idx> ] }
```
- Example
```javascript
/* our collection looks like this:
{ "_id" : 1, "name" : "dave123", favorites: [ "chocolate", "cake", "butter", "apples" ] }
{ "_id" : 2, "name" : "li", favorites: [ "apples", "pudding", "pie" ] }
{ "_id" : 3, "name" : "ahn", favorites: [ "pears", "pecans", "chocolate", "cherries" ] }
{ "_id" : 4, "name" : "ty", favorites: [ "ice cream" ] }
*/

// multiply price with quantitiy
const pipeline = [
   {
     $project:
      {
         name: 1,
         first: { $arrayElemAt: [ "$favorites", 0 ] },
         last: { $arrayElemAt: [ "$favorites", -1 ] }
      }
   }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
The operation returns the following results:
{ "_id" : 1, "name" : "dave123", "first" : "chocolate", "last" : "apples" }
{ "_id" : 2, "name" : "li", "first" : "apples", "last" : "pie" }
{ "_id" : 3, "name" : "ahn", "first" : "pears", "last" : "cherries" }
{ "_id" : 4, "name" : "ty", "first" : "ice cream", "last" : "ice cream" }
*/
```


<br><br>
____________________________________________________
<br><br>
- $arrayToObject	Converts an array of key value pairs to a document. (https://docs.mongodb.com/manual/reference/operator/aggregation/arrayToObject/#exp._S_arrayToObject)


<br><br>
____________________________________________________
<br><br>
- $concatArrays	Concatenates arrays to return the concatenated array. (https://docs.mongodb.com/manual/reference/operator/aggregation/concatArrays/#exp._S_concatArrays)




<br><br>
____________________________________________________
<br><br>
- $filter	Selects a subset of the array to return an array with only the elements that match the filter condition. (https://docs.mongodb.com/manual/reference/operator/aggregation/filter/#exp._S_filter)
- Syntax:
```javascript
{ $filter: { input: <array>, as: <string>, cond: <expression> } }
```
- Example:
```javascript
/* // Source collection:
[
{
   _id: 0,
   items: [
     { item_id: 43, quantity: 2, price: 10 },
     { item_id: 2, quantity: 1, price: 240 }
   ]
},
{
   _id: 1,
   items: [
     { item_id: 23, quantity: 3, price: 110 },
     { item_id: 103, quantity: 4, price: 5 },
     { item_id: 38, quantity: 1, price: 300 }
   ]
},
{
    _id: 2,
    items: [
       { item_id: 4, quantity: 1, price: 23 }
    ]
}
]
*/

const pipeline = [
   {
      $project: {
         items: {
            $filter: {
               input: "$items",
               as: "item",
               cond: { $gte: [ "$$item.price", 100 ] }
            }
         }
      }
   }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
[
{
   "_id" : 0,
   "items" : [
      { "item_id" : 2, "quantity" : 1, "price" : 240 }
   ]
},
{
   "_id" : 1,
   "items" : [
      { "item_id" : 23, "quantity" : 3, "price" : 110 },
      { "item_id" : 38, "quantity" : 1, "price" : 300 }
   ]
},
{ "_id" : 2, "items" : [ ] }
]
*/
```



<br><br>
____________________________________________________
<br><br>
- $first	Returns the first array element. Distinct from $first accumulator. (https://docs.mongodb.com/manual/reference/operator/aggregation/first-array-element/#exp._S_first)


<br><br>
____________________________________________________
<br><br>
- $in	Returns a boolean indicating whether a specified value is in an array. (https://docs.mongodb.com/manual/reference/operator/aggregation/in/#exp._S_in)


<br><br>
____________________________________________________
<br><br>
- $indexOfArray	Searches an array for an occurrence of a specified value and returns the array index of the first occurrence. If the substring is not found, returns -1. (https://docs.mongodb.com/manual/reference/operator/aggregation/indexOfArray/#exp._S_indexOfArray)


<br><br>
____________________________________________________
<br><br>
- $isArray	Determines if the operand is an array. Returns a boolean. (https://docs.mongodb.com/manual/reference/operator/aggregation/isArray/#exp._S_isArray)
- Syntax:
```javascript
{ $isArray: [ <expression> ] }
```
- Example:
```javascript
/* // Source collection:
[
  { "_id" : 1, instock: [ "chocolate" ], ordered: [ "butter", "apples" ] },
  { "_id" : 2, instock: [ "apples", "pudding", "pie" ] },
  { "_id" : 3, instock: [ "pears", "pecans"], ordered: [ "cherries" ] },
  { "_id" : 4, instock: [ "ice cream" ], ordered: [ ] },
]
*/

const pipeline = [
   { $project:
      { items:
          { $cond:
            {
              if: { $and: [ { $isArray: "$instock" }, { $isArray: "$ordered" } ] },
              then: { $concatArrays: [ "$instock", "$ordered" ] },
              else: "One or more fields is not an array."
            }
          }
      }
   }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
[
  { "_id" : 1, "items" : [ "chocolate", "butter", "apples" ] },
  { "_id" : 2, "items" : "One or more fields is not an array." },
  { "_id" : 3, "items" : [ "pears", "pecans", "cherries" ] },
  { "_id" : 4, "items" : [ "ice cream" ] },
]
*/
```


<br><br>
____________________________________________________
<br><br>
- $last	Returns the last array element. Distinct from $last accumulator. (https://docs.mongodb.com/manual/reference/operator/aggregation/last-array-element/#exp._S_last)


<br><br>
____________________________________________________
<br><br>
- $map	Applies a subexpression to each element of an array and returns the array of resulting values in order. Accepts named parameters. (https://docs.mongodb.com/manual/reference/operator/aggregation/map/#exp._S_map)
```javascript
/* our collection looks like this:
  { _id: 1, quizzes: [ 5, 6, 7 ] },
  { _id: 2, quizzes: [ ] },
  { _id: 3, quizzes: [ 3, 8, 9 ] }
*/

// The following aggregation operation uses $map with the $add expression to increment each element in the quizzes array by 2.
const pipeline = [
      { $project:
         { adjustedGrades:
            {
              $map:
                 {
                   input: "$quizzes",
                   as: "grade",
                   in: { $add: [ "$$grade", 2 ] }
                 }
            }
         }
      }
   ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) { /* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
The operation returns the following results:
  { "_id" : 1, "adjustedGrades" : [ 7, 8, 9 ] }
  { "_id" : 2, "adjustedGrades" : [ ] }
  { "_id" : 3, "adjustedGrades" : [ 5, 10, 11 ] }
*/
```


<br><br>
____________________________________________________
<br><br>
- $objectToArray	Converts a document to an array of documents representing key-value pairs. (https://docs.mongodb.com/manual/reference/operator/aggregation/objectToArray/#exp._S_objectToArray)


<br><br>
____________________________________________________
<br><br>
- $range	Outputs an array containing a sequence of integers according to user-defined inputs. (https://docs.mongodb.com/manual/reference/operator/aggregation/range/#exp._S_range)



<br><br>
____________________________________________________
<br><br>
- $reduce	Applies an expression to each element in an array and combines them into a single value. (https://docs.mongodb.com/manual/reference/operator/aggregation/reduce/#exp._S_reduce)
- **$$this** refers to the current element in the array
- **$$value** refers to the accumulator value
- Options:
```javascript
/*
- input | array | Can be any valid expression that resolves to an array. For more information on expressions, see Expressions.
- initialValue | expression | The initial cumulative value set before in is applied to the first element of the input array.
- in | 	expression | A valid expression that $reduce applies to each element in the input array in left-to-right order. Wrap the input value with $reverseArray to yield the equivalent of applying the combining expression from right-to-left.
*/
```
- Syntax:
```javascript
{
    $reduce: {
        input: <array>,
        initialValue: <expression>,
        in: <expression>
    }
}
```
- Example:
```javascript
/* // source collection:
[
  {_id:1, "type":"die", "experimentId":"r5", "description":"Roll a 5", "eventNum":1, "probability":0.16666666666667},
  {_id:2, "type":"card", "experimentId":"d3rc", "description":"Draw 3 red cards", "eventNum":1, "probability":0.5},
  {_id:3, "type":"card", "experimentId":"d3rc", "description":"Draw 3 red cards", "eventNum":2, "probability":0.49019607843137},
  {_id:4, "type":"card", "experimentId":"d3rc", "description":"Draw 3 red cards", "eventNum":3, "probability":0.48},
  {_id:5, "type":"die", "experimentId":"r16", "description":"Roll a 1 then a 6", "eventNum":1, "probability":0.16666666666667},
  {_id:6, "type":"die", "experimentId":"r16", "description":"Roll a 1 then a 6", "eventNum":2, "probability":0.16666666666667},
  {_id:7, "type":"card", "experimentId":"dak", "description":"Draw an ace, then a king", "eventNum":1, "probability":0.07692307692308},
  {_id:8, "type":"card", "experimentId":"dak", "description":"Draw an ace, then a king", "eventNum":2, "probability":0.07843137254902},
]
*/


/*
1. Use $group to group by the experimentId and use $push to create an array with the probability of each event.
2. Use $reduce with $multiply to multiply and combine the elements of probabilityArr into a single value and project it.
*/
const pipeline = [
    {
      $group: {
        _id: "$experimentId",
        "probabilityArr": { $push: "$probability" }
      }
    },
    {
      $project: {
        "description": 1,
        "results": {
          $reduce: {
            input: "$probabilityArr",
            initialValue: 1,
            in: { $multiply: [ "$$value", "$$this" ] }
          }
        }
      }
    }
  ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* result:
[
  { "_id" : "dak", "results" : 0.00603318250377101 },
  { "_id" : "r5", "results" : 0.16666666666667 },
  { "_id" : "r16", "results" : 0.027777777777778886 },
  { "_id" : "d3rc", "results" : 0.11764705882352879 },
]
*/





// ------ OTHER EXAMPLES -------
const pipeline = [{
   $reduce: {
      input: [ 1, 2, 3, 4 ],
      initialValue: { sum: 5, product: 2 },
      in: {
         sum: { $add : ["$$value.sum", "$$this"] },
         product: { $multiply: [ "$$value.product", "$$this" ] }
      }
   }
}];

/* result:
{ "sum" : 15, "product" : 48 }
*/



const pipeline = [{
   $reduce: {
      input: [ [ 3, 4 ], [ 5, 6 ] ],
      initialValue: [ 1, 2 ],
      in: { $concatArrays : ["$$value", "$$this"] }
   }
}];

/* result:
[ 1, 2, 3, 4, 5, 6 ]
*/
```


<br><br>
____________________________________________________
<br><br>
- $reverseArray	Returns an array with the elements in reverse order. (https://docs.mongodb.com/manual/reference/operator/aggregation/reverseArray/#exp._S_reverseArray)


<br><br>
____________________________________________________
<br><br>
- $size	Returns the number of elements in the array. Accepts a single expression as argument. (https://docs.mongodb.com/manual/reference/operator/aggregation/size/#exp._S_size)


<br><br>
____________________________________________________
<br><br>
- $slice	Returns a subset of an array. (https://docs.mongodb.com/manual/reference/operator/aggregation/slice/#exp._S_slice)


<br><br>
____________________________________________________
<br><br>
- $zip	Merge two arrays together. (https://docs.mongodb.com/manual/reference/operator/aggregation/zip/#exp._S_zip)
- Syntax:
```javascript
{
    $zip: {
        inputs: [ <array expression1>,  ... ],
        useLongestLength: <boolean>,
        defaults:  <array expression>
    }
}
```
- Options:
```javascript
/*
inputs | An array of expressions that resolve to arrays. The elements of these input arrays combine to form the arrays of the output array

useLongestLength | A boolean which specifies whether the length of the longest array determines the number of arrays in the output array.

defaults | An array of default element values to use if the input arrays have different lengths. You must specify useLongestLength: true along with this field, or else $zip will return an error.
*/
```
- Example:
```javascript
/* // source collection:
[
  { matrix: [[1, 2], [2, 3], [3, 4]] },
  { matrix: [[8, 7], [7, 6], [5, 4]] },
]
*/


// To compute the transpose of each 3x2 matrix in this collection, you can use the following aggregation operation:
const pipeline = [{
  $project: {
    _id: false,
    transposed: {
      $zip: {
        inputs: [
          { $arrayElemAt: [ "$matrix", 0 ] },
          { $arrayElemAt: [ "$matrix", 1 ] },
          { $arrayElemAt: [ "$matrix", 2 ] },
        ]
      }
    }
  }
}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* result:
[
  { "transposed" : [ [ 1, 2, 3 ], [ 2, 3, 4 ] ] },
  { "transposed" : [ [ 8, 7, 5 ], [ 7, 6, 4 ] ] },
]
*/
```











<br><br>
____________________________________________________
____________________________________________________
<br><br>









#### Boolean Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#boolean-expression-operators)
- $and	Returns true only when all its expressions evaluate to true. Accepts any number of argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/and/#exp._S_and)


<br><br>
____________________________________________________
<br><br>
- $not	Returns the boolean value that is the opposite of its argument expression. Accepts a single argument expression. (https://docs.mongodb.com/manual/reference/operator/aggregation/not/#exp._S_not)


<br><br>
____________________________________________________
<br><br>
- $or	Returns true when any of its expressions evaluates to true. Accepts any number of argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/or/#exp._S_or)









<br><br>
____________________________________________________
____________________________________________________
<br><br>








#### Comparison Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#comparison-expression-operators)
- $cmp	Returns 0 if the two values are equivalent, 1 if the first value is greater than the second, and -1 if the first value is less than the second. (https://docs.mongodb.com/manual/reference/operator/aggregation/cmp/#exp._S_cmp)



<br><br>
____________________________________________________
<br><br>
- $gt	Returns true if the first value is greater than the second. (https://docs.mongodb.com/manual/reference/operator/aggregation/gt/#exp._S_gt)


<br><br>
____________________________________________________
<br><br>
- $gte	Returns true if the first value is greater than or equal to the second. (https://docs.mongodb.com/manual/reference/operator/aggregation/gte/#exp._S_gte)


<br><br>
____________________________________________________
<br><br>
- $lt	Returns true if the first value is less than the second. (https://docs.mongodb.com/manual/reference/operator/aggregation/lt/#exp._S_lt)


<br><br>
____________________________________________________
<br><br>
- $lte	Returns true if the first value is less than or equal to the second. (https://docs.mongodb.com/manual/reference/operator/aggregation/lte/#exp._S_lte)


<br><br>
____________________________________________________
<br><br>
- $ne	Returns true if the values are not equivalent. (https://docs.mongodb.com/manual/reference/operator/aggregation/ne/#exp._S_ne)










<br><br>
____________________________________________________
____________________________________________________
<br><br>










#### Conditional Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#conditional-expression-operators)
- $cond	A ternary operator that evaluates one expression, and depending on the result, returns the value of one of the other two expressions. Accepts either three expressions in an ordered list or three named parameters. (https://docs.mongodb.com/manual/reference/operator/aggregation/cond/#exp._S_cond)
- $cond is very usefully when and expression would get null if it does not exist.
- Syntax:
```javascript
// syntax #1
{ $cond: { if: <boolean-expression>, then: <true-case>, else: <false-case> } }

// syntax #2
{ $cond: [ <boolean-expression>, <true-case>, <false-case> ] }
```
- Example:
```javascript
/* our collection looks like this:
[
  { "_id" : 1, "item" : "abc1", qty: 300 },
  { "_id" : 2, "item" : "abc2", qty: 200 },
  { "_id" : 3, "item" : "xyz1", qty: 250 },
]
*/

// The following aggregation operation uses $map with the $add expression to increment each element in the quizzes array by 2.
// method 1
const pipeline = [
      {
         $project:
           {
             item: 1,
             discount:
               {
                 $cond: { if: { $gte: [ "$qty", 250 ] }, then: 30, else: 20 }
               }
           }
      }
   ];
   
// method 2 (short)   
const pipeline = [
     {
         $project:
           {
             item: 1,
             discount:
               {
                 $cond: [ { $gte: [ "$qty", 250 ] }, 30, 20 ]
               }
           }
      }
   ]


// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
// The operation returns the following results:
[
  { "_id" : 1, "item" : "abc1", "discount" : 30 },
  { "_id" : 2, "item" : "abc2", "discount" : 20 },
  { "_id" : 3, "item" : "xyz1", "discount" : 30 },
]
*/
```


<br><br>
____________________________________________________
<br><br>
- $ifNull	Returns either the non-null result of the first expression or the result of the second expression if the first expression results in a null result. Null result encompasses instances of undefined values or missing fields. Accepts two expressions as arguments. The result of the second expression can be null. (https://docs.mongodb.com/manual/reference/operator/aggregation/ifNull/#exp._S_ifNull)


<br><br>
____________________________________________________
<br><br>
- $switch	Evaluates a series of case expressions. When it finds an expression which evaluates to true, $switch executes a specified expression and breaks out of the control flow. (https://docs.mongodb.com/manual/reference/operator/aggregation/switch/#exp._S_switch)












<br><br>
____________________________________________________
____________________________________________________
<br><br>








#### Custom Aggregation Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#custom-aggregation-expression-operators)
- $accumulator - Defines a custom accumulator function. (https://docs.mongodb.com/manual/reference/operator/aggregation/accumulator/#grp._S_accumulator)


<br><br>
____________________________________________________
<br><br>
- $function	- Defines a custom function. (https://docs.mongodb.com/manual/reference/operator/aggregation/function/#exp._S_function)












<br><br>
____________________________________________________
____________________________________________________
<br><br>









#### Data Size Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#data-size-operators)
- $binarySize	Returns the size of a given string or binary data value’s content in bytes. (https://docs.mongodb.com/manual/reference/operator/aggregation/binarySize/#exp._S_binarySize)


<br><br>
____________________________________________________
<br><br>
- $bsonSize	Returns the size in bytes of a given document (i.e. bsontype Object) when encoded as BSON. (https://docs.mongodb.com/manual/reference/operator/aggregation/bsonSize/#exp._S_bsonSize)












<br><br>
____________________________________________________
____________________________________________________
<br><br>












#### Date Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#date-expression-operators)
- $dateFromParts	Constructs a BSON Date object given the date’s constituent parts. (https://docs.mongodb.com/manual/reference/operator/aggregation/dateFromParts/#exp._S_dateFromParts)


<br><br>
____________________________________________________
<br><br>
- $dateFromString	Converts a date/time string to a date object. (https://docs.mongodb.com/manual/reference/operator/aggregation/dateFromString/#exp._S_dateFromString)


<br><br>
____________________________________________________
<br><br>
- $dateToParts	Returns a document containing the constituent parts of a date. (https://docs.mongodb.com/manual/reference/operator/aggregation/dateToParts/#exp._S_dateToParts)


<br><br>
____________________________________________________
<br><br>
- $dateToString	Returns the date as a formatted string. (https://docs.mongodb.com/manual/reference/operator/aggregation/dateToString/#exp._S_dateToString)


<br><br>
____________________________________________________
<br><br>
- $dayOfMonth	Returns the day of the month for a date as a number between 1 and 31. (https://docs.mongodb.com/manual/reference/operator/aggregation/dayOfMonth/#exp._S_dayOfMonth)


<br><br>
____________________________________________________
<br><br>
- $dayOfWeek	Returns the day of the week for a date as a number between 1 (Sunday) and 7 (Saturday). (https://docs.mongodb.com/manual/reference/operator/aggregation/dayOfWeek/#exp._S_dayOfWeek)


<br><br>
____________________________________________________
<br><br>
- $dayOfYear	Returns the day of the year for a date as a number between 1 and 366 (leap year). (https://docs.mongodb.com/manual/reference/operator/aggregation/dayOfYear/#exp._S_dayOfYear)


<br><br>
____________________________________________________
<br><br>
- $hour	Returns the hour for a date as a number between 0 and 23. (https://docs.mongodb.com/manual/reference/operator/aggregation/hour/#exp._S_hour)


<br><br>
____________________________________________________
<br><br>
- $isoDayOfWeek	Returns the weekday number in ISO 8601 format, ranging from 1 (for Monday) to 7 (for Sunday). (https://docs.mongodb.com/manual/reference/operator/aggregation/isoDayOfWeek/#exp._S_isoDayOfWeek)


<br><br>
____________________________________________________
<br><br>
- $isoWeek	Returns the week number in ISO 8601 format, ranging from 1 to 53. Week numbers start at 1 with the week (Monday through Sunday) that contains the year’s first Thursday. (https://docs.mongodb.com/manual/reference/operator/aggregation/isoWeek/#exp._S_isoWeek)


<br><br>
____________________________________________________
<br><br>
- $isoWeekYear	Returns the year number in ISO 8601 format. The year starts with the Monday of week 1 (ISO 8601) and ends with the Sunday of the last week (ISO 8601). (https://docs.mongodb.com/manual/reference/operator/aggregation/isoWeekYear/#exp._S_isoWeekYear)


<br><br>
____________________________________________________
<br><br>
- $millisecond	Returns the milliseconds of a date as a number between 0 and 999. (https://docs.mongodb.com/manual/reference/operator/aggregation/millisecond/#exp._S_millisecond)


<br><br>
____________________________________________________
<br><br>
- $minute	Returns the minute for a date as a number between 0 and 59. (https://docs.mongodb.com/manual/reference/operator/aggregation/minute/#exp._S_minute)


<br><br>
____________________________________________________
<br><br>
- $month	Returns the month for a date as a number between 1 (January) and 12 (December). (https://docs.mongodb.com/manual/reference/operator/aggregation/month/#exp._S_month)


<br><br>
____________________________________________________
<br><br>
- $second	Returns the seconds for a date as a number between 0 and 60 (leap seconds). (https://docs.mongodb.com/manual/reference/operator/aggregation/second/#exp._S_second)


<br><br>
____________________________________________________
<br><br>
- $toDate	Converts value to a Date. (https://docs.mongodb.com/manual/reference/operator/aggregation/toDate/#exp._S_toDate)


<br><br>
____________________________________________________
<br><br>
- $week	Returns the week number for a date as a number between 0 (the partial week that precedes the first Sunday of the year) and 53 (leap year). (https://docs.mongodb.com/manual/reference/operator/aggregation/week/#exp._S_week)


<br><br>
____________________________________________________
<br><br>
- $year	Returns the year for a date as a number (e.g. 2014). (https://docs.mongodb.com/manual/reference/operator/aggregation/year/#exp._S_year)


<br><br>
____________________________________________________
<br><br>
- $add	Adds numbers and a date to return a new date. If adding numbers and a date, treats the numbers as milliseconds. Accepts any number of argument expressions, but at most, one expression can resolve to a date. (https://docs.mongodb.com/manual/reference/operator/aggregation/add/#exp._S_add)


<br><br>
____________________________________________________
<br><br>
- $subtract	Returns the result of subtracting the second value from the first. If the two values are dates, return the difference in milliseconds. If the two values are a date and a number in milliseconds, return the resulting date. Accepts two argument expressions. If the two values are a date and a number, specify the date argument first as it is not meaningful to subtract a date from a number. (https://docs.mongodb.com/manual/reference/operator/aggregation/subtract/#exp._S_subtract)














<br><br>
____________________________________________________
____________________________________________________
<br><br>









#### Literal Expression Operator (https://docs.mongodb.com/manual/reference/operator/aggregation/#literal-expression-operator)
- $literal	Return a value without parsing. Use for values that the aggregation pipeline may interpret as an expression. For example, use a $literal expression to a string that starts with a $ to avoid parsing as a field path. (https://docs.mongodb.com/manual/reference/operator/aggregation/literal/#exp._S_literal)











<br><br>
____________________________________________________
____________________________________________________
<br><br>










#### Miscellaneous Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#miscellaneous-operators)
- $rand	Returns a random float between 0 and 1 (https://docs.mongodb.com/manual/reference/operator/aggregation/rand/#exp._S_rand)


<br><br>
____________________________________________________
<br><br>
- $sampleRate	Randomly select documents at a given rate. Although the exact number of documents selected varies on each run, the quantity chosen approximates the sample rate expressed as a percentage of the total number of documents. (https://docs.mongodb.com/manual/reference/operator/aggregation/sampleRate/#exp._S_sampleRate)











<br><br>
____________________________________________________
____________________________________________________
<br><br>









#### Object Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#object-expression-operators)
- $mergeObjects	Combines multiple documents into a single document. (https://docs.mongodb.com/manual/reference/operator/aggregation/mergeObjects/#exp._S_mergeObjects)


<br><br>
____________________________________________________
<br><br>
- $objectToArray	Converts a document to an array of documents representing key-value pairs. (https://docs.mongodb.com/manual/reference/operator/aggregation/objectToArray/#exp._S_objectToArray)












<br><br>
____________________________________________________
____________________________________________________
<br><br>








#### Set Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#set-expression-operators)
- $allElementsTrue	Returns true if no element of a set evaluates to false, otherwise, returns false. Accepts a single argument expression. (https://docs.mongodb.com/manual/reference/operator/aggregation/allElementsTrue/#exp._S_allElementsTrue)


<br><br>
____________________________________________________
<br><br>
- $anyElementTrue	Returns true if any elements of a set evaluate to true; otherwise, returns false. Accepts a single argument expression. (https://docs.mongodb.com/manual/reference/operator/aggregation/anyElementTrue/#exp._S_anyElementTrue)


<br><br>
____________________________________________________
<br><br>
- $setDifference	Returns a set with elements that appear in the first set but not in the second set; i.e. performs a relative complement of the second set relative to the first. Accepts exactly two argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/setDifference/#exp._S_setDifference)


<br><br>
____________________________________________________
<br><br>
- $setEquals	Returns true if the input sets have the same distinct elements. Accepts two or more argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/setEquals/#exp._S_setEquals)



<br><br>
____________________________________________________
<br><br>
- $setIntersection	Returns a set with elements that appear in all of the input sets. Accepts any number of argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/setIntersection/#exp._S_setIntersection)
- Syntax:
```javascript
{ $setIntersection: [ <array1>, <array2>, ... ] }
```
- Example:
```javascript
/* our collection looks like this:
{ "_id" : 1, "A" : [ "red", "blue" ], "B" : [ "red", "blue" ] }
{ "_id" : 2, "A" : [ "red", "blue" ], "B" : [ "blue", "red", "blue" ] }
{ "_id" : 3, "A" : [ "red", "blue" ], "B" : [ "red", "blue", "green" ] }
{ "_id" : 4, "A" : [ "red", "blue" ], "B" : [ "green", "red" ] }
{ "_id" : 5, "A" : [ "red", "blue" ], "B" : [ ] }
{ "_id" : 6, "A" : [ "red", "blue" ], "B" : [ [ "red" ], [ "blue" ] ] }
{ "_id" : 7, "A" : [ "red", "blue" ], "B" : [ [ "red", "blue" ] ] }
{ "_id" : 8, "A" : [ ], "B" : [ ] }
{ "_id" : 9, "A" : [ ], "B" : [ "red" ] }
*/

// The following aggregation operation uses $map with the $add expression to increment each element in the quizzes array by 2.
const pipeline = [
     { $project: { A: 1, B: 1, commonToBoth: { $setIntersection: [ "$A", "$B" ] }, _id: 0 } }
   ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
// The operation returns the following results:
{ "A" : [ "red", "blue" ], "B" : [ "red", "blue" ], "commonToBoth" : [ "blue", "red" ] }
{ "A" : [ "red", "blue" ], "B" : [ "blue", "red", "blue" ], "commonToBoth" : [ "blue", "red" ] }
{ "A" : [ "red", "blue" ], "B" : [ "red", "blue", "green" ], "commonToBoth" : [ "blue", "red" ] }
{ "A" : [ "red", "blue" ], "B" : [ "green", "red" ], "commonToBoth" : [ "red" ] }
{ "A" : [ "red", "blue" ], "B" : [ ], "commonToBoth" : [ ] }
{ "A" : [ "red", "blue" ], "B" : [ [ "red" ], [ "blue" ] ], "commonToBoth" : [ ] }
{ "A" : [ "red", "blue" ], "B" : [ [ "red", "blue" ] ], "commonToBoth" : [ ] }
{ "A" : [ ], "B" : [ ], "commonToBoth" : [ ] }
{ "A" : [ ], "B" : [ "red" ], "commonToBoth" : [ ] }
*/
```


<br><br>
____________________________________________________
<br><br>
- $setIsSubset	Returns true if all elements of the first set appear in the second set, including when the first set equals the second set; i.e. not a strict subset. Accepts exactly two argument expressions. (https://docs.mongodb.com/manual/reference/operator/aggregation/setIsSubset/#exp._S_setIsSubset)


<br><br>
____________________________________________________
<br><br>
- $setUnion	Returns a set with elements that appear in any of the input sets. (https://docs.mongodb.com/manual/reference/operator/aggregation/setUnion/#exp._S_setUnion)




















<br><br>
____________________________________________________
____________________________________________________
<br><br>








#### String Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#string-expression-operators)
- $concat	Concatenates any number of strings. (https://docs.mongodb.com/manual/reference/operator/aggregation/concat/#exp._S_concat)
- Syntax:
```javascript
{ $concat: [ <expression1>, <expression2>, ... ] }
```
- Example:
```javascript
/* source collection:
[
  { "_id" : 1, "item" : "ABC1", quarter: "13Q1", "description" : "product 1" },
  { "_id" : 2, "item" : "ABC2", quarter: "13Q4", "description" : "product 2" },
  { "_id" : 3, "item" : "XYZ1", quarter: "14Q2", "description" : null },
]
*/

// The following operation uses the $concat operator to concatenate the item field and the description field with a ” - ” delimiter.
const pipeline = [
      { $project: { itemDescription: { $concat: [ "$item", " - ", "$description" ] } } }
   ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
// result:
[
  { "_id" : 1, "itemDescription" : "ABC1 - product 1" },
  { "_id" : 2, "itemDescription" : "ABC2 - product 2" },
  { "_id" : 3, "itemDescription" : null },
]
*/
```



<br><br>
____________________________________________________
<br><br>
- $dateFromString	Converts a date/time string to a date object. (https://docs.mongodb.com/manual/reference/operator/aggregation/dateFromString/#exp._S_dateFromString)


<br><br>
____________________________________________________
<br><br>
- $dateToString	Returns the date as a formatted string. (https://docs.mongodb.com/manual/reference/operator/aggregation/dateToString/#exp._S_dateToString)


<br><br>
____________________________________________________
<br><br>
- $indexOfBytes	Searches a string for an occurrence of a substring and returns the UTF-8 byte index of the first occurrence. If the substring is not found, returns -1. (https://docs.mongodb.com/manual/reference/operator/aggregation/indexOfBytes/#exp._S_indexOfBytes)


<br><br>
____________________________________________________
<br><br>
- $indexOfCP	Searches a string for an occurrence of a substring and returns the UTF-8 code point index of the first occurrence. If the substring is not found, returns -1 (https://docs.mongodb.com/manual/reference/operator/aggregation/indexOfCP/#exp._S_indexOfCP)


<br><br>
____________________________________________________
<br><br>
- $ltrim	Removes whitespace or the specified characters from the beginning of a string. (https://docs.mongodb.com/manual/reference/operator/aggregation/ltrim/#exp._S_ltrim)


<br><br>
____________________________________________________
<br><br>
- $regexFind	Applies a regular expression (regex) to a string and returns information on the first matched substring. (https://docs.mongodb.com/manual/reference/operator/aggregation/regexFind/#exp._S_regexFind)


<br><br>
____________________________________________________
<br><br>
- $regexFindAll	Applies a regular expression (regex) to a string and returns information on the all matched substrings. (https://docs.mongodb.com/manual/reference/operator/aggregation/regexFindAll/#exp._S_regexFindAll)


<br><br>
____________________________________________________
<br><br>
- $regexMatch	Applies a regular expression (regex) to a string and returns a boolean that indicates if a match is found or not. (https://docs.mongodb.com/manual/reference/operator/aggregation/regexMatch/#exp._S_regexMatch)


<br><br>
____________________________________________________
<br><br>
- $replaceOne	Replaces the first instance of a matched string in a given input. (https://docs.mongodb.com/manual/reference/operator/aggregation/replaceOne/#exp._S_replaceOne)


<br><br>
____________________________________________________
<br><br>
- $replaceAll	Replaces all instances of a matched string in a given input. (https://docs.mongodb.com/manual/reference/operator/aggregation/replaceAll/#exp._S_replaceAll)


<br><br>
____________________________________________________
<br><br>
- $rtrim	Removes whitespace or the specified characters from the end of a string. (https://docs.mongodb.com/manual/reference/operator/aggregation/rtrim/#exp._S_rtrim)





<br><br>
____________________________________________________
<br><br>
- $split	Splits a string into substrings based on a delimiter. Returns an array of substrings. If the delimiter is not found within the string, returns an array containing the original string. (https://docs.mongodb.com/manual/reference/operator/aggregation/split/#exp._S_split)
- Syntax:
```javascript
{ $split: [ <string expression>, <delimiter> ] }
```
- Example:
```javascript
/* source collection:
[
  { "_id" : 1, "city" : "Berkeley, CA", "qty" : 648 },
  { "_id" : 2, "city" : "Bend, OR", "qty" : 491 },
  { "_id" : 3, "city" : "Kensington, CA", "qty" : 233 },
  { "_id" : 4, "city" : "Eugene, OR", "qty" : 842 },
  { "_id" : 5, "city" : "Reno, NV", "qty" : 655 },
  { "_id" : 6, "city" : "Portland, OR", "qty" : 408 },
  { "_id" : 7, "city" : "Sacramento, CA", "qty" : 574 },
]
*/

// The following operation uses the $concat operator to concatenate the item field and the description field with a ” - ” delimiter.
const pipeline = [
  { $project : { city_state : { $split: ["$city", ", "] }, qty : 1 } },
  { $unwind : "$city_state" },
  { $match : { city_state : /[A-Z]{2}/ } },
  { $group : { _id: { "state" : "$city_state" }, total_qty : { "$sum" : "$qty" } } },
  { $sort : { total_qty : -1 } }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
// result:
[
  { "_id" : { "state" : "OR" }, "total_qty" : 1741 },
  { "_id" : { "state" : "CA" }, "total_qty" : 1455 },
  { "_id" : { "state" : "NV" }, "total_qty" : 655 },
]
*/
```



<br><br>
____________________________________________________
<br><br>
- $strLenBytes	Returns the number of UTF-8 encoded bytes in a string. (https://docs.mongodb.com/manual/reference/operator/aggregation/strLenBytes/#exp._S_strLenBytes)


<br><br>
____________________________________________________
<br><br>
- $strLenCP	Returns the number of UTF-8 code points in a string. (https://docs.mongodb.com/manual/reference/operator/aggregation/strLenCP/#exp._S_strLenCP)


<br><br>
____________________________________________________
<br><br>
- $strcasecmp	Performs case-insensitive string comparison and returns: 0 if two strings are equivalent, 1 if the first string is greater than the second, and -1 if the first string is less than the second. (https://docs.mongodb.com/manual/reference/operator/aggregation/strcasecmp/#exp._S_strcasecmp)


<br><br>
____________________________________________________
<br><br>
- $substrBytes	Returns the substring of a string. Starts with the character at the specified UTF-8 byte index (zero-based) in the string and continues for the specified number of bytes. (https://docs.mongodb.com/manual/reference/operator/aggregation/substrBytes/#exp._S_substrBytes)


<br><br>
____________________________________________________
<br><br>
- $substrCP	Returns the substring of a string. Starts with the character at the specified UTF-8 code point (CP) index (zero-based) in the string and continues for the number of code points specified. (https://docs.mongodb.com/manual/reference/operator/aggregation/substrCP/#exp._S_substrCP)


<br><br>
____________________________________________________
<br><br>
- $toLower	Converts a string to lowercase. Accepts a single argument expression. (https://docs.mongodb.com/manual/reference/operator/aggregation/toLower/#exp._S_toLower)


<br><br>
____________________________________________________
<br><br>
- $toString	Converts value to a string. (https://docs.mongodb.com/manual/reference/operator/aggregation/toString/#exp._S_toString)


<br><br>
____________________________________________________
<br><br>
- $trim	Removes whitespace or the specified characters from the beginning and end of a string. (https://docs.mongodb.com/manual/reference/operator/aggregation/trim/#exp._S_trim)


<br><br>
____________________________________________________
<br><br>
- $toUpper	Converts a string to uppercase. Accepts a single argument expression. (https://docs.mongodb.com/manual/reference/operator/aggregation/toUpper/#exp._S_toUpper)















<br><br>
____________________________________________________
____________________________________________________
<br><br>











#### Text Expression Operator (https://docs.mongodb.com/manual/reference/operator/aggregation/#text-expression-operator)
- $meta	Access available per-document metadata related to the aggregation operation. (https://docs.mongodb.com/manual/reference/operator/aggregation/meta/#exp._S_meta)

















<br><br>
____________________________________________________
____________________________________________________
<br><br>











#### Trigonometry Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#trigonometry-expression-operators)
- $sin	Returns the sine of a value that is measured in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/sin/#exp._S_sin)


<br><br>
____________________________________________________
<br><br>
- $cos	Returns the cosine of a value that is measured in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/cos/#exp._S_cos)


<br><br>
____________________________________________________
<br><br>
- $tan	Returns the tangent of a value that is measured in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/tan/#exp._S_tan)


<br><br>
____________________________________________________
<br><br>
- $asin	Returns the inverse sin (arc sine) of a value in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/asin/#exp._S_asin)


<br><br>
____________________________________________________
<br><br>
- $acos	Returns the inverse cosine (arc cosine) of a value in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/acos/#exp._S_acos)


<br><br>
____________________________________________________
<br><br>
- $atan	Returns the inverse tangent (arc tangent) of a value in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/atan/#exp._S_atan)


<br><br>
____________________________________________________
<br><br>
- $atan2	Returns the inverse tangent (arc tangent) of y / x in radians, where y and x are the first and second values passed to the expression respectively. (https://docs.mongodb.com/manual/reference/operator/aggregation/atan2/#exp._S_atan2)


<br><br>
____________________________________________________
<br><br>
- $asinh	Returns the inverse hyperbolic sine (hyperbolic arc sine) of a value in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/asinh/#exp._S_asinh)


<br><br>
____________________________________________________
<br><br>
- $acosh	Returns the inverse hyperbolic cosine (hyperbolic arc cosine) of a value in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/acosh/#exp._S_acosh)


<br><br>
____________________________________________________
<br><br>
- $atanh	Returns the inverse hyperbolic tangent (hyperbolic arc tangent) of a value in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/atanh/#exp._S_atanh)


<br><br>
____________________________________________________
<br><br>
- $sinh	Returns the hyperbolic sine of a value that is measured in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/sinh/#exp._S_sinh)


<br><br>
____________________________________________________
<br><br>
- $cosh	Returns the hyperbolic cosine of a value that is measured in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/cosh/#exp._S_cosh)


<br><br>
____________________________________________________
<br><br>
- $tanh	Returns the hyperbolic tangent of a value that is measured in radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/tanh/#exp._S_tanh)


<br><br>
____________________________________________________
<br><br>
- $degreesToRadians	Converts a value from degrees to radians. (https://docs.mongodb.com/manual/reference/operator/aggregation/degreesToRadians/#exp._S_degreesToRadians)


<br><br>
____________________________________________________
<br><br>
- $radiansToDegrees	Converts a value from radians to degrees. (https://docs.mongodb.com/manual/reference/operator/aggregation/radiansToDegrees/#exp._S_radiansToDegrees)












<br><br>
____________________________________________________
____________________________________________________
<br><br>








#### Type Expression Operators (https://docs.mongodb.com/manual/reference/operator/aggregation/#type-expression-operators)
- $convert	Converts a value to a specified type. (https://docs.mongodb.com/manual/reference/operator/aggregation/convert/#exp._S_convert)


<br><br>
____________________________________________________
<br><br>
- $isNumber	Returns boolean true if the specified expression resolves to an integer, decimal, double, or long. Returns boolean false if the expression resolves to any other BSON type, null, or a missing field. (https://docs.mongodb.com/manual/reference/operator/aggregation/isNumber/#exp._S_isNumber)


<br><br>
____________________________________________________
<br><br>
- $toBool	Converts value to a boolean. (https://docs.mongodb.com/manual/reference/operator/aggregation/toBool/#exp._S_toBool)


<br><br>
____________________________________________________
<br><br>
- $toDate	Converts value to a Date. (https://docs.mongodb.com/manual/reference/operator/aggregation/toDate/#exp._S_toDate)


<br><br>
____________________________________________________
<br><br>
- $toDecimal	Converts value to a Decimal128. (https://docs.mongodb.com/manual/reference/operator/aggregation/toDecimal/#exp._S_toDecimal)


<br><br>
____________________________________________________
<br><br>
- $toDouble	Converts value to a double. (https://docs.mongodb.com/manual/reference/operator/aggregation/toDouble/#exp._S_toDouble)


<br><br>
____________________________________________________
<br><br>
- $toInt	Converts value to an integer. (https://docs.mongodb.com/manual/reference/operator/aggregation/toInt/#exp._S_toInt)


<br><br>
____________________________________________________
<br><br>
- $toLong	Converts value to a long. (https://docs.mongodb.com/manual/reference/operator/aggregation/toLong/#exp._S_toLong)


<br><br>
____________________________________________________
<br><br>
- $toObjectId	Converts value to an ObjectId. (https://docs.mongodb.com/manual/reference/operator/aggregation/toObjectId/#exp._S_toObjectId)


<br><br>
____________________________________________________
<br><br>
- $toString	Converts value to a string. (https://docs.mongodb.com/manual/reference/operator/aggregation/toString/#exp._S_toString)


<br><br>
____________________________________________________
<br><br>
- $type	Return the BSON data type of the field. (https://docs.mongodb.com/manual/reference/operator/aggregation/type/#exp._S_type)














<br><br>
____________________________________________________
____________________________________________________
<br><br>






#### Accumulators ($group) (https://docs.mongodb.com/manual/reference/operator/aggregation/#accumulators-group)
- https://docs.mongodb.com/manual/reference/operator/aggregation/group/#pipe._S_group

<br><br>
- $accumulator	Returns the result of a user-defined accumulator function. (https://docs.mongodb.com/manual/reference/operator/aggregation/accumulator/#grp._S_accumulator)



<br><br>
____________________________________________________
<br><br>
- $addToSet	Returns an array of unique expression values for each group. Order of the array elements is undefined. (https://docs.mongodb.com/manual/reference/operator/aggregation/addToSet/#grp._S_addToSet)
- Syntax:
```javascript
{ $addToSet: <expression> }
```
- Example:
```javascript
/* our collection looks like this:
[
  { "_id" : 1, "item" : "abc", "price" : 10, "quantity" : 2, "date" : ISODate("2014-01-01T08:00:00Z") },
  { "_id" : 2, "item" : "jkl", "price" : 20, "quantity" : 1, "date" : ISODate("2014-02-03T09:00:00Z") },
  { "_id" : 3, "item" : "xyz", "price" : 5, "quantity" : 5, "date" : ISODate("2014-02-03T09:05:00Z") },
  { "_id" : 4, "item" : "abc", "price" : 10, "quantity" : 10, "date" : ISODate("2014-02-15T08:00:00Z") },
  { "_id" : 5, "item" : "xyz", "price" : 5, "quantity" : 10, "date" : ISODate("2014-02-15T09:12:00Z") },
]
*/

// The following aggregation operation uses $map with the $add expression to increment each element in the quizzes array by 2.
const pipeline = [
     {
       $group:
         {
           _id: { day: { $dayOfYear: "$date"}, year: { $year: "$date" } },
           itemsSold: { $addToSet: "$item" }
         }
     }
   ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
// The operation returns the following results:
[
  { "_id" : { "day" : 46, "year" : 2014 }, "itemsSold" : [ "xyz", "abc" ] },
  { "_id" : { "day" : 34, "year" : 2014 }, "itemsSold" : [ "xyz", "jkl" ] },
  { "_id" : { "day" : 1, "year" : 2014 }, "itemsSold" : [ "abc" ] },
]
*/
```



<br><br>
____________________________________________________
<br><br>
- $avg	Returns an average of numerical values. Ignores non-numeric values. (https://docs.mongodb.com/manual/reference/operator/aggregation/avg/#grp._S_avg)
- In easy words when you use $avg inside of $group and you got multiple documents with the same _id then it will count all of those together and then get the average value. In $project where we just got a unique ID it will work default.
- $avg is available in the following stages:
<br>$group
<br>$project
<br>$addFields (Available starting in MongoDB 3.4)
<br>$set (Available starting in MongoDB 4.2)
<br>$replaceRoot (Available starting in MongoDB 3.4)
<br>$replaceWith (Available starting in MongoDB 4.2)
<br>$match stage that includes an $expr expression

<br><br>
- Syntax:
```javascript
{ $avg: <expression> }

// or

{ $avg: [ <expression1>, <expression2> ... ]  }
```
- Example:
```javascript
/* our collection looks like this:
[
  { "_id" : 1, "item" : "abc", "price" : 10, "quantity" : 2, "date" : ISODate("2014-01-01T08:00:00Z") },
  { "_id" : 2, "item" : "jkl", "price" : 20, "quantity" : 1, "date" : ISODate("2014-02-03T09:00:00Z") },
  { "_id" : 3, "item" : "xyz", "price" : 5, "quantity" : 5, "date" : ISODate("2014-02-03T09:05:00Z") },
  { "_id" : 4, "item" : "abc", "price" : 10, "quantity" : 10, "date" : ISODate("2014-02-15T08:00:00Z") },
  { "_id" : 5, "item" : "xyz", "price" : 5, "quantity" : 10, "date" : ISODate("2014-02-15T09:12:00Z") },
]
*/

// Grouping the documents by the item field, the following operation uses the $max accumulator to compute the maximum total amount and maximum quantity for each group of documents.
const pipeline = [
     {
       $group:
         {
           _id: "$item",
           avgAmount: { $avg: { $multiply: [ "$price", "$quantity" ] } },
           avgQuantity: { $avg: "$quantity" }
         }
     }
   ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
// The operation returns the following results:
[
  { "_id" : "xyz", "avgAmount" : 37.5, "avgQuantity" : 7.5 },
  { "_id" : "jkl", "avgAmount" : 20, "avgQuantity" : 1 },
  { "_id" : "abc", "avgAmount" : 60, "avgQuantity" : 6 },
]
*/











// ------ EXAMPLE #2 $project --------
/* our collection looks like this:
[
  { "_id": 1, "quizzes": [ 10, 6, 7 ], "labs": [ 5, 8 ], "final": 80, "midterm": 75 },
  { "_id": 2, "quizzes": [ 9, 10 ], "labs": [ 8, 8 ], "final": 95, "midterm": 80 },
  { "_id": 3, "quizzes": [ 4, 5, 5 ], "labs": [ 6, 5 ], "final": 78, "midterm": 70 },
]
*/

// Grouping the documents by the item field, the following operation uses the $max accumulator to compute the maximum total amount and maximum quantity for each group of documents.
const pipeline = [
   { $project: { quizAvg: { $avg: "$quizzes"}, labAvg: { $avg: "$labs" }, examAvg: { $avg: [ "$final", "$midterm" ] } } }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
// The operation returns the following results:
[
  { "_id" : 1, "quizAvg" : 7.666666666666667, "labAvg" : 6.5, "examAvg" : 77.5 },
  { "_id" : 2, "quizAvg" : 9.5, "labAvg" : 8, "examAvg" : 87.5 },
  { "_id" : 3, "quizAvg" : 4.666666666666667, "labAvg" : 5.5, "examAvg" : 74 },
]
*/
```


<br><br>
____________________________________________________
<br><br>
- $first	Returns a value from the first document for each group. Order is only defined if the documents are in a defined order. Distinct from the $first array operator. (https://docs.mongodb.com/manual/reference/operator/aggregation/first/#grp._S_first)


<br><br>
____________________________________________________
<br><br>
- $last	Returns a value from the last document for each group. Order is only defined if the documents are in a defined order. Distinct from the $last array operator. (https://docs.mongodb.com/manual/reference/operator/aggregation/last/#grp._S_last)


<br><br>
____________________________________________________
<br><br>
- $max	Returns the highest expression value for each group. (https://docs.mongodb.com/manual/reference/operator/aggregation/max/#grp._S_max)
- In easy words. When you use $max inside of $group where multiple documents has the same _id then $max will compare all elements and get the max total amount. If you use $project you got a unique _id so it will only process the current collection.
- $max is available in the following stages:
<br>$group
<br>$project
<br>$addFields (Available starting in MongoDB 3.4)
<br>$set (Available starting in MongoDB 4.2)
<br>$replaceRoot (Available starting in MongoDB 3.4)
<br>$replaceWith (Available starting in MongoDB 4.2)
<br>$match stage that includes an $expr expression
<br><br>
- Syntax:
```javascript
{ $max: [ <expression1>, <expression2> ... ]  }
```
- Example:
```javascript
/* our collection looks like this:
[
  { "_id" : 1, "item" : "abc", "price" : 10, "quantity" : 2, "date" : ISODate("2014-01-01T08:00:00Z") },
  { "_id" : 2, "item" : "jkl", "price" : 20, "quantity" : 1, "date" : ISODate("2014-02-03T09:00:00Z") },
  { "_id" : 3, "item" : "xyz", "price" : 5, "quantity" : 5, "date" : ISODate("2014-02-03T09:05:00Z") },
  { "_id" : 4, "item" : "abc", "price" : 10, "quantity" : 10, "date" : ISODate("2014-02-15T08:00:00Z") },
  { "_id" : 5, "item" : "xyz", "price" : 5, "quantity" : 10, "date" : ISODate("2014-02-15T09:05:00Z") },
]
*/

// Grouping the documents by the item field, the following operation uses the $max accumulator to compute the maximum total amount and maximum quantity for each group of documents.
const pipeline = [
     {
       $group:
         {
           _id: "$item",
           maxTotalAmount: { $max: { $multiply: [ "$price", "$quantity" ] } },
           maxQuantity: { $max: "$quantity" }
         }
     }
   ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
// The operation returns the following results:
[
  { "_id" : "xyz", "maxTotalAmount" : 50, "maxQuantity" : 10 },
  { "_id" : "jkl", "maxTotalAmount" : 20, "maxQuantity" : 1 },
  { "_id" : "abc", "maxTotalAmount" : 100, "maxQuantity" : 10 },
]
*/










// ------ EXAMPLE #2 ------
/* our collection looks like this:
[
  { "_id": 1, "quizzes": [ 10, 6, 7 ], "labs": [ 5, 8 ], "final": 80, "midterm": 75 },
  { "_id": 2, "quizzes": [ 9, 10 ], "labs": [ 8, 8 ], "final": 95, "midterm": 80 },
  { "_id": 3, "quizzes": [ 4, 5, 5 ], "labs": [ 6, 5 ], "final": 78, "midterm": 70 },
]
*/

// The following example uses the $max in the $project stage to calculate the maximum quiz scores, the maximum lab scores, and the maximum of the final and the midterm:
const pipeline = [
   { $project: { quizMax: { $max: "$quizzes"}, labMax: { $max: "$labs" }, examMax: { $max: [ "$final", "$midterm" ] } } }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
// The operation returns the following results:
[
  { "_id" : 1, "quizMax" : 10, "labMax" : 8, "examMax" : 80 },
  { "_id" : 2, "quizMax" : 10, "labMax" : 8, "examMax" : 95 },
  { "_id" : 3, "quizMax" : 5, "labMax" : 6, "examMax" : 78 },
]
*/
```


<br><br>
____________________________________________________
<br><br>
- $mergeObjects	Returns a document created by combining the input documents for each group. (https://docs.mongodb.com/manual/reference/operator/aggregation/mergeObjects/#exp._S_mergeObjects)


<br><br>
____________________________________________________
<br><br>
- $min	Returns the lowest expression value for each group. (https://docs.mongodb.com/manual/reference/operator/aggregation/min/#grp._S_min)
- In easy words. When you use $min inside of $group where multiple documents has the same _id then $min will compare all elements and get the min total amount. If you use $project you got a unique _id so it will only process the current collection.
- Syntax:
```javascript
{ $min: <expression> }
```
- Example:
```javascript
/* our collection looks like this:
[
  { "_id" : 1, "item" : "abc", "price" : 10, "quantity" : 2, "date" : ISODate("2014-01-01T08:00:00Z") },
  { "_id" : 2, "item" : "jkl", "price" : 20, "quantity" : 1, "date" : ISODate("2014-02-03T09:00:00Z") },
  { "_id" : 3, "item" : "xyz", "price" : 5, "quantity" : 5, "date" : ISODate("2014-02-03T09:05:00Z") },
  { "_id" : 4, "item" : "abc", "price" : 10, "quantity" : 10, "date" : ISODate("2014-02-15T08:00:00Z") },
  { "_id" : 5, "item" : "xyz", "price" : 5, "quantity" : 10, "date" : ISODate("2014-02-15T09:05:00Z") },
]
*/

// Grouping the documents by the item field, the following operation uses the $min accumulator to compute the minimum amount and minimum quantity for each grouping.
const pipeline = [
     {
       $group:
         {
           _id: "$item",
           minQuantity: { $min: "$quantity" }
         }
     }
   ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
// The operation returns the following results:
[
  { "_id" : "xyz", "minQuantity" : 5 },
  { "_id" : "jkl", "minQuantity" : 1 },
  { "_id" : "abc", "minQuantity" : 2 },
]
*/











// ----- EXAMPLE #2 -------
/* our collection looks like this:
[
  { "_id": 1, "quizzes": [ 10, 6, 7 ], "labs": [ 5, 8 ], "final": 80, "midterm": 75 },
  { "_id": 2, "quizzes": [ 9, 10 ], "labs": [ 8, 8 ], "final": 95, "midterm": 80 },
  { "_id": 3, "quizzes": [ 4, 5, 5 ], "labs": [ 6, 5 ], "final": 78, "midterm": 70 },
]
*/

// Grouping the documents by the item field, the following operation uses the $min accumulator to compute the minimum amount and minimum quantity for each grouping.
const pipeline = [
   { $project: { quizMin: { $min: "$quizzes"}, labMin: { $min: "$labs" }, examMin: { $min: [ "$final", "$midterm" ] } } }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
// The operation returns the following results:
[
  { "_id" : 1, "quizMin" : 6, "labMin" : 5, "examMin" : 75 },
  { "_id" : 2, "quizMin" : 9, "labMin" : 8, "examMin" : 80 },
  { "_id" : 3, "quizMin" : 4, "labMin" : 5, "examMin" : 70 },
]
*/

```


<br><br>
____________________________________________________
<br><br>
- **$push**	Returns an array of expression values for each group. (https://docs.mongodb.com/manual/reference/operator/aggregation/push/#grp._S_push)
- Syntax:
```javascript
{ $push: <expression> }
```
- Example:
```javascript
/* our collection looks like this:
[
  { "_id" : 1, "item" : "abc", "price" : 10, "quantity" : 2, "date" : ISODate("2014-01-01T08:00:00Z") },
  { "_id" : 2, "item" : "jkl", "price" : 20, "quantity" : 1, "date" : ISODate("2014-02-03T09:00:00Z") },
  { "_id" : 3, "item" : "xyz", "price" : 5, "quantity" : 5, "date" : ISODate("2014-02-03T09:05:00Z") },
  { "_id" : 4, "item" : "abc", "price" : 10, "quantity" : 10, "date" : ISODate("2014-02-15T08:00:00Z") },
  { "_id" : 5, "item" : "xyz", "price" : 5, "quantity" : 10, "date" : ISODate("2014-02-15T09:05:00Z") },
  { "_id" : 6, "item" : "xyz", "price" : 5, "quantity" : 5, "date" : ISODate("2014-02-15T12:05:10Z") },
  { "_id" : 7, "item" : "xyz", "price" : 5, "quantity" : 10, "date" : ISODate("2014-02-15T14:12:12Z") },
]
*/

// The following example calculates the standard deviation of each quiz:
const pipeline = [
     {
       $group:
         {
           _id: { day: { $dayOfYear: "$date"}, year: { $year: "$date" } },
           itemsSold: { $push:  { item: "$item", quantity: "$quantity" } }
         }
     }
   ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
// The operation returns the following results:
[
{
   "_id" : { "day" : 46, "year" : 2014 },
   "itemsSold" : [
      { "item" : "abc", "quantity" : 10 },
      { "item" : "xyz", "quantity" : 10 },
      { "item" : "xyz", "quantity" : 5 },
      { "item" : "xyz", "quantity" : 10 }
   ]
},
{
   "_id" : { "day" : 34, "year" : 2014 },
   "itemsSold" : [
      { "item" : "jkl", "quantity" : 1 },
      { "item" : "xyz", "quantity" : 5 }
   ]
},
{
   "_id" : { "day" : 1, "year" : 2014 },
   "itemsSold" : [ { "item" : "abc", "quantity" : 2 } ]
}
]
*/
```




<br><br>
____________________________________________________
<br><br>
- **$stdDevPop**	Returns the population standard deviation of the input values. (https://docs.mongodb.com/manual/reference/operator/aggregation/stdDevPop/#grp._S_stdDevPop)
- $stdDevPop is available in the in the following stages:
<br>$group
<br>$project
<br>$addFields (Available starting in MongoDB 3.4)
<br>$set (Available starting in MongoDB 4.2)
<br>$replaceRoot (Available starting in MongoDB 3.4)
<br>$replaceWith (Available starting in MongoDB 4.2)
<br>$match stage that includes an $expr expression
<br><br>
- Syntax:
```javascript
{ $stdDevPop: <expression> }

// or

{ $stdDevPop: [ <expression1>, <expression2> ... ]  }
```
- Example:
```javascript
/* our collection looks like this:
[
  { "_id" : 1, "name" : "dave123", "quiz" : 1, "score" : 85 },
  { "_id" : 2, "name" : "dave2", "quiz" : 1, "score" : 90 },
  { "_id" : 3, "name" : "ahn", "quiz" : 1, "score" : 71 },
  { "_id" : 4, "name" : "li", "quiz" : 2, "score" : 96 },
  { "_id" : 5, "name" : "annT", "quiz" : 2, "score" : 77 },
  { "_id" : 6, "name" : "ty", "quiz" : 2, "score" : 82 },
]
*/

// The following example calculates the standard deviation of each quiz:
const pipeline = [
   { $group: { _id: "$quiz", stdDev: { $stdDevPop: "$score" } } }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
// The operation returns the following results:
[
  { "_id" : 2, "stdDev" : 8.04155872120988 },
  { "_id" : 1, "stdDev" : 8.04155872120988 },
]
*/






// ----- EXAMPLE #2 $project ---------
/* our collection looks like this:
[
 {
      "_id" : 1,
      "scores" : [
         { "name" : "dave123", "score" : 85 },
         { "name" : "dave2", "score" : 90 },
         { "name" : "ahn", "score" : 71 }
      ]
   },
   {
      "_id" : 2,
      "scores" : [
         { "name" : "li", "quiz" : 2, "score" : 96 },
         { "name" : "annT", "score" : 77 },
         { "name" : "ty", "score" : 82 }
      ]
   }
]
*/

// The following example calculates the standard deviation of each quiz:
const pipeline = [
   { $project: { stdDev: { $stdDevPop: "$scores.score" } } }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
// The operation returns the following results:
[
  { "_id" : 1, "stdDev" : 8.04155872120988 },
  { "_id" : 2, "stdDev" : 8.04155872120988 },
]
*/
```


<br><br>
____________________________________________________
<br><br>
- **$stdDevSamp**	Returns the sample standard deviation of the input values. (https://docs.mongodb.com/manual/reference/operator/aggregation/stdDevSamp/#grp._S_stdDevSamp)
- $stdDevSamp is available in the in the following stages:
<br>$group
<br>$project
<br>$addFields (Available starting in MongoDB 3.4)
<br>$set (Available starting in MongoDB 4.2)
<br>$replaceRoot (Available starting in MongoDB 3.4)
<br>$replaceWith (Available starting in MongoDB 4.2)
<br>$match stage that includes an $expr expression
<br><br>
- Syntax:
```javascript
{ $stdDevSamp: <expression> }

// or

{ $stdDevSamp: [ <expression1>, <expression2> ... ]  }
```
```javascript
/* // source collection
[
  {_id: 0, username: "user0", age: 20},
  {_id: 1, username: "user1", age: 42},
  {_id: 2, username: "user2", age: 28},
  // ...
]
*/

const pipeline = [
      { $sample: { size: 100 } },
      { $group: { _id: null, ageStdDev: { $stdDevSamp: "$age" } } }
   ];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
[
  { "_id" : null, "ageStdDev" : 7.811258386185771 }
]
*/
```


<br><br>
____________________________________________________
<br><br>
- **$sum**	Returns a sum of numerical values. Ignores non-numeric values. (https://docs.mongodb.com/manual/reference/operator/aggregation/sum/#grp._S_sum)
- In easy words each match sum will get called. If you use **count: {$sum: 1}** then each new match counts gets +1
- Syntax:
```javascript
{$sum: <expression>}
```
- Example:
```javascript
/* our collection looks like this:
[
  { "_id" : 1, "item" : "abc", "price" : 10, "quantity" : 2, "date" : ISODate("2014-01-01T08:00:00Z") },
  { "_id" : 2, "item" : "jkl", "price" : 20, "quantity" : 1, "date" : ISODate("2014-02-03T09:00:00Z") },
  { "_id" : 3, "item" : "xyz", "price" : 5, "quantity" : 5, "date" : ISODate("2014-02-03T09:05:00Z") },
  { "_id" : 4, "item" : "abc", "price" : 10, "quantity" : 10, "date" : ISODate("2014-02-15T08:00:00Z") },
  { "_id" : 5, "item" : "xyz", "price" : 5, "quantity" : 10, "date" : ISODate("2014-02-15T09:05:00Z") },
]
*/

// Grouping the documents by the day and the year of the date field, the following operation uses the $sum accumulator to compute the total amount and the count for each group of documents.
const pipeline = [
     {
       $group:
         {
           _id: { day: { $dayOfYear: "$date"}, year: { $year: "$date" } },
           totalAmount: { $sum: { $multiply: [ "$price", "$quantity" ] } },
           count: { $sum: 1 }
         }
     }
   ]

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/*
// The operation returns the following results:
[
  { "_id" : { "day" : 46, "year" : 2014 }, "totalAmount" : 150, "count" : 2 },
  { "_id" : { "day" : 34, "year" : 2014 }, "totalAmount" : 45, "count" : 2 },
  { "_id" : { "day" : 1, "year" : 2014 }, "totalAmount" : 20, "count" : 1 },
]
*/
```
<br><br>















<br><br>
____________________________________________________
____________________________________________________
<br><br>










#### Accumulators (in Other Stages)
- $avg	Returns an average of the specified expression or list of expressions for each document. Ignores non-numeric values. (https://docs.mongodb.com/manual/reference/operator/aggregation/avg/#grp._S_avg)


<br><br>
____________________________________________________
<br><br>
- $max	Returns the maximum of the specified expression or list of expressions for each document (https://docs.mongodb.com/manual/reference/operator/aggregation/max/#grp._S_max)


<br><br>
____________________________________________________
<br><br>
- $min	Returns the minimum of the specified expression or list of expressions for each document (https://docs.mongodb.com/manual/reference/operator/aggregation/min/#grp._S_min)


<br><br>
____________________________________________________
<br><br>
- $stdDevPop	Returns the population standard deviation of the input values. (https://docs.mongodb.com/manual/reference/operator/aggregation/stdDevPop/#grp._S_stdDevPop)


<br><br>
____________________________________________________
<br><br>
- $stdDevSamp	Returns the sample standard deviation of the input values. (https://docs.mongodb.com/manual/reference/operator/aggregation/stdDevSamp/#grp._S_stdDevSamp)












<br><br>
____________________________________________________
____________________________________________________
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

// method #4 - .itcount (https://docs.mongodb.com/manual/reference/method/cursor.itcount/)
// itcount() is similar to cursor.count(), but actually executes the query on an existing iterator, exhausting its contents in the process.
const numMovies = await movies.aggregate([...]).itcount();

// method 4 - $count inside of aggregation pipeline
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




#### allowDiskUse (https://docs.mongodb.com/manual/reference/method/cursor.allowDiskUse/)
- allowDiskUse() allows MongoDB to use temporary files on disk to store data exceeding the 100 megabyte system memory limit while processing a blocking sort operation. If MongoDB requires using more than 100 megabytes of system memory for the blocking sort operation, MongoDB returns an error unless the query specifies cursor.allowDiskUse().
```javascript
// ------- AGGREGATE -------

// sort results by year
const pipeline = [
  [{ $sort: {year: 1}}],
  {allowDiskUse: true}
];

// callback
collection.aggregate(...pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(...pipeline).toArray({});





// ------- CURSOR -------
const query = {"payload.discount": {$exists: true}};

// await
const r = await collection.findOne(query).allowDiskUse();
```











































<br><br>
____________________________________________________
____________________________________________________
<br><br>




#### .createIndex() (https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/)
- Syntax:
```javascript
collection.createIndex({comments: "text"});
```

<br><br>
- text index (https://docs.mongodb.com/manual/core/index-text/#index-feature-text)
- When you create a text index you can later to search operations on them. You can also text index multiple fields
```javascript
collection.createIndex({subject: "text", comments: "text"});

// create text index on all fields in collection
// collection.createIndex( { "$**": "text" } )

collection.find( { $text: { $search: "bake coffee cake" } } )

/* // result:
[
  { "_id" : 2, "subject" : "Coffee Shopping", "author" : "efg", "views" : 5 },
  { "_id" : 7, "subject" : "coffee and cream", "author" : "efg", "views" : 10 },
  { "_id" : 1, "subject" : "coffee", "author" : "xyz", "views" : 50 },
  { "_id" : 3, "subject" : "Baking a cake", "author" : "abc", "views" : 90 },
  { "_id" : 4, "subject" : "baking", "author" : "xyz", "views" : 100 },
]
*/
```

- Options:
```javascript
/*
- keys | document | A document that contains the field and value pairs where the field is the index key and the value describes the type of index for that field. For an ascending index on a field, specify a value of 1; for descending index, specify a value of -1. Starting in 3.6, you cannot specify * as the index name.

- otions | document | Optional. A document that contains a set of options that controls the creation of the index.

- commitQuorum	| integer or string | Optional. The minimum number of data-bearing voting replica set members (i.e. commit quorum), including the primary, that must report a successful index build before the primary marks the indexes as ready. A “voting” member is any replica set member where members[n].votes is greater than 0.
*/
```
Example:
```javascript
// For example, the collection myColl has an index on a string field category with the collation locale "fr".
const ar = [{category: 1}, {collation: {locale: "fr"}}];

// callback
collection.createIndex(...ar).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.createIndex(...ar).toArray({});


// The following query operation, which specifies the same collation as the index, can use the index:
collection.find({category: "cafe"}).collation({locale: "fr"});

// However, the following query operation, which by default uses the “simple” binary collator, cannot use the index:
collection.find({category: "cafe"});
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





<br><br>


#### do regex text search recursive on any property of the document
```javascript
let resultAr = []
const recursiveSearch = async function(query) {
    await collection.find().forEach(function(items) {
        var i = 0;
        console.log('items: ' + JSON.stringify(items));

        var recursiveFunc = async function(itemsArray, itemKey) {
            var keyValue = itemsArray[itemKey];
            console.log('keyValue: ' + keyValue);

            if(typeof keyValue === "object") {
                Object.keys(keyValue).forEach(function(keyValueKey) {
                    recursiveFunc(keyValue, keyValueKey);
                });
            } else{
                if(keyValue.match(query)) {
                    console.log('match found: ' + keyValue);
                    resultAr.push(keyValue);
                }
            }
        };

        Object.keys(items).forEach(key => {
            console.log('key: ' + key);
            recursiveFunc(items, key);
        });
    });
};

await recursiveSearch(/https:[/][/]s3-eu-central-1[.]amazonaws[.]com[/][^'"`\]\\]+/);
console.log('resultAr: ' + resultAr);
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

<br><br>

## Options
- https://docs.mongodb.com/manual/reference/method/db.collection.aggregate/
```javascript
- explain | Optional. Specifies to return the information on the processing of the pipeline
- allowDiskUse | Optional. Enables writing to temporary files. When set to true, aggregation operations can write data to the _tmp subdirectory in the dbPath directory. See Perform Large Sort Operation with External Sort for an example.
- cursor | Optional. Specifies the initial batch size for the cursor. The value of the cursor field is a document with the field batchSize. See Specify an Initial Batch Size for syntax and example.
- maxTimeMS | Optional. Specifies a time limit in milliseconds for processing operations on a cursor. If you do not specify a value for maxTimeMS, operations will not time out. A value of 0 explicitly specifies the default unbounded behavior.
- bypassDocumentValidation | Optional. Applicable only if you specify the $out or $merge aggregation stages.
- readConcern | Optional. Specifies the read concern.
- writeConcern | Optional. A document that expresses the write concern to use with the $out or $merge stage.
- collation | Optional. Specifies the collation to use for the operation. Collation allows users to specify language-specific rules for string comparison, such as rules for lettercase and accent marks.
- hint | Optional. The index to use for the aggregation. The index is on the initial collection/view against which the aggregation is run.
- comment | Optional. Users can specify an arbitrary string to help trace the operation through the database profiler, currentOp, and logs.
- 
```
<br><br>

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

## Performance
- https://www.youtube.com/watch?v=BlPqPoyWk1k

<br><br>
#### General Rules
- Try first to create indexes (.createIndex()). If this is not enough use allowDiskUse. allowDiskUse is way slower than using RAM. Notice that allowDiskUse does not work $graphLookup
- $match the indexes
- Put $sort stages to the top as soon as you can
- Put $limit stages to the top as soon as you can. Also try to put it over $sort
- Put $limit before $skip
- When you use $group try to project all fields there instead of using later a $project stage.
- Use accumulator expressions $map, $reduce and $filter in $project before an $unwind, if possible

<br><br>
#### Good 2 Know
- Results are limited to 16MB. If you get over this size you should use $limit and $project
- Stages are limited to . The best to stay under this limit is by using index. If you still over the limit you can use allowDiskUse to bypass this limit.

<br><br>
#### "Realtime" Processing
- Provide data for applications and should return as fast as possible to not disturb the user experience.
- Query performance is more important.


<br><br>
#### Batch Processing
- Provide data for analytics as example for a cron job and can take more time if needed.
- Query performance is less important.


<br><br>
#### Index Usage
- If any aggregation stage does not support index then the following stages will also not support it.


<br><br>
#### Determine how aggregation queries are executed (**{explain: true}**)
```javascript
/* // source collection:
[
  { "_id" : 1, "title" : "The Pillars of Society", "artist" : "Grosz", "year" : 1926, "tags" : [ "painting", "satire", "Expressionism", "caricature" ] },
  { "_id" : 2, "title" : "Melancholy III", "artist" : "Munch", "year" : 1902, "tags" : [ "woodcut", "Expressionism" ] },
  { "_id" : 3, "title" : "Dancer", "artist" : "Miro", "year" : 1925, "tags" : [ "oil", "Surrealism", "painting" ] },
  { "_id" : 4, "title" : "The Great Wave off Kanagawa", "artist" : "Hokusai", "tags" : [ "woodblock", "ukiyo-e" ] },
  { "_id" : 5, "title" : "The Persistence of Memory", "artist" : "Dali", "year" : 1931, "tags" : [ "Surrealism", "painting", "oil" ] },
  { "_id" : 6, "title" : "Composition VII", "artist" : "Kandinsky", "year" : 1913, "tags" : [ "oil", "painting", "abstract" ] },
  { "_id" : 7, "title" : "The Scream", "artist" : "Munch", "year" : 1893, "tags" : [ "Expressionism", "painting", "oil" ] },
  { "_id" : 8, "title" : "Blue Flower", "artist" : "O'Keefe", "year" : 1918, "tags" : [ "abstract", "painting" ] },
]
*/

// The following operation unwinds the tags array and uses the $sortByCount stage to count the number of documents associated with each tag:
const pipeline = [
[{$unwind: "$tags"},  {$sortByCount: "$tags"}],
{explain: true}.
];

// callback
collection.aggregate(...pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(...pipeline).toArray({});
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

#### match multiple values
```javascript
/* // source collection
[
  {
    '_id': '12345678',
    'used': 0,
    'name': 'John',
    'date': [
       'year': 2015
     ]
  },
  {
    '_id': '12345678',
    'used': 0,
    'name': 'Smith',
    'date': [
       'year': 2015
     ]
  },
  {
    '_id': '12345678',
    'used': 0,
    'name': 'Lena',
    'date': [
       'year': 2015
     ]
  }
]
*/

const pipeline = [{
    $match: {
        name: {
            $in: ['John', 'Smith']
        }
    }
}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result
[
  {
    '_id': '12345678',
    'used': 0,
    'name': 'John',
    'date': [
       'year': 2015
     ]
  },
  {
    '_id': '12345678',
    'used': 0,
    'name': 'Smith',
    'date': [
       'year': 2015
     ]
  }
]
*/
```




















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

#### choose all documents
- We can use **'_id': null** or **'_id': ''**
```javascript
const pipeline = [{'$group': {
                   '_id': null,
                   'count': {'$sum': 1}
                 }}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* operation will return:
[{_id:null, count:327}] // count will be the total amount of documents in our collection. Of course collection.count() or similiar stuff would achieve the same thing.
*/



// ----- MORE PRODUCTION RELATED EXAMPLE ------
// first we match all fields that contain specific url. If this field does not exist or is different it will be ignored. Then after this we can use {'_id': null} to group all documents and get the average value.
const pipeline = [
  {$match: {url: 'anyURL'}},
  {$group: {'_id': null, 'averageData': {$avg: '$anyfield'}}},
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});
```

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



#### keep all fields while grouping
```javascript
// method #1 - Manually define the fields you want to keep by using $first
const pipeline = db.test.aggregate([{
      $group: {
         _id : '$name',
         name : { $first: '$name' },
         age : { $first: '$age' },
         sex : { $first: '$sex' },
         province : { $first: '$province' },
         city : { $first: '$city' },
         area : { $first: '$area' },
         address : { $first: '$address' },
         count : { $sum: 1 },
      }
    }]);
   
   
// method #2 - Create object by using $$ROOT
const pipeline = [
  {
    $group: {
      _id: '$name',
      user: { $first: '$$ROOT' },
      count: { $sum: 1 }
    },
  },
  {
    $replaceRoot: {
      newRoot: { $mergeObjects: [{ count: '$count' }, '$user'] }
    }
  }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});
```

<br><br>









































<br><br>
<br><br>


## check if array is empty
```javascript
/* // source collection
[
  {_id: '123', year: [2015, 2016]},
  {_id: '123', year: []},
]
*/

const pipeline = [{$match: {{year: {$size: 1}}}}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* result:
[
  {_id: '123', year: [2015, 2016]},
]
*/
```

<br><br>


## check if string is empty
```javascript
/* // source collection
[
  {_id: '123', year: '2016'},
  {_id: '123', year: ''},
]
*/

const pipeline = [{$match: {{year: {"$exists" : true, "$ne" : ""}}}}];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */ });

// async
const r = await collection.aggregate(pipeline).toArray({});

/* result:
[
  {_id: '123', year: '2016'},
]
*/
```

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



























































































<br><br>

____________________________________________________
____________________________________________________

<br><br>


# Facets

<br><br>

## Single Facet Query
- https://www.youtube.com/watch?v=NMyDE4oWwpg
```javascript

// example #1
const pipeline = [
  {"$match": { "$text": {"$search": "network"}}},
  {"$sortByCount": "$offices.city"}
];

// example #2
const pipeline = [
  {"$unwind": "$offices"},
  {"$project": { "_id": "$name", "hq": "$offices.city"}},
  {"$sortByCount": "$hq"},
  {"$sort": {"_id":-1}},
  {"$limit": 100}
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});
```








<br><br>

## Multiple Facets
- https://www.youtube.com/watch?v=Cz2ioKSF2rw
```javascript
/* // source collection:
[
{ "_id" : 1, "title" : "The Pillars of Society", "artist" : "Grosz", "year" : 1926,
  "price" : NumberDecimal("199.99"),
  "tags" : [ "painting", "satire", "Expressionism", "caricature" ] }.
{ "_id" : 2, "title" : "Melancholy III", "artist" : "Munch", "year" : 1902,
  "price" : NumberDecimal("280.00"),
  "tags" : [ "woodcut", "Expressionism" ] }.
{ "_id" : 3, "title" : "Dancer", "artist" : "Miro", "year" : 1925,
  "price" : NumberDecimal("76.04"),
  "tags" : [ "oil", "Surrealism", "painting" ] }.
{ "_id" : 4, "title" : "The Great Wave off Kanagawa", "artist" : "Hokusai",
  "price" : NumberDecimal("167.30"),
  "tags" : [ "woodblock", "ukiyo-e" ] }.
{ "_id" : 5, "title" : "The Persistence of Memory", "artist" : "Dali", "year" : 1931,
  "price" : NumberDecimal("483.00"),
  "tags" : [ "Surrealism", "painting", "oil" ] }.
{ "_id" : 6, "title" : "Composition VII", "artist" : "Kandinsky", "year" : 1913,
  "price" : NumberDecimal("385.00"),
  "tags" : [ "oil", "painting", "abstract" ] }.
{ "_id" : 7, "title" : "The Scream", "artist" : "Munch", "year" : 1893,
  "tags" : [ "Expressionism", "painting", "oil" ] }.
{ "_id" : 8, "title" : "Blue Flower", "artist" : "O'Keefe", "year" : 1918,
  "price" : NumberDecimal("118.42"),
  "tags" : [ "abstract", "painting" ] }
]
*/

// skip first 2 documents in natural order
const pipeline = [
  {
    $facet: {
      "categorizedByTags": [
        { $unwind: "$tags" },
        { $sortByCount: "$tags" }
      ],
      "categorizedByPrice": [
        // Filter out documents without a price e.g., _id: 7
        { $match: { price: { $exists: 1 } } },
        {
          $bucket: {
            groupBy: "$price",
            boundaries: [  0, 150, 200, 300, 400 ],
            default: "Other",
            output: {
              "count": { $sum: 1 },
              "titles": { $push: "$title" }
            }
          }
        }
      ],
      "categorizedByYears(Auto)": [
        {
          $bucketAuto: {
            groupBy: "$year",
            buckets: 4
          }
        }
      ]
    }
  }
];

// callback
collection.aggregate(pipeline).toArray(function(e, docs) {/* .. */});

// async
const r = await collection.aggregate(pipeline).toArray({});

/* // result:
{
  "categorizedByYears(Auto)" : [
    // First bucket includes the document without a year, e.g., _id: 4
    { "_id" : { "min" : null, "max" : 1902 }, "count" : 2 },
    { "_id" : { "min" : 1902, "max" : 1918 }, "count" : 2 },
    { "_id" : { "min" : 1918, "max" : 1926 }, "count" : 2 },
    { "_id" : { "min" : 1926, "max" : 1931 }, "count" : 2 }
  ],
  "categorizedByPrice" : [
    {
      "_id" : 0,
      "count" : 2,
      "titles" : [
        "Dancer",
        "Blue Flower"
      ]
    },
    {
      "_id" : 150,
      "count" : 2,
      "titles" : [
        "The Pillars of Society",
        "The Great Wave off Kanagawa"
      ]
    },
    {
      "_id" : 200,
      "count" : 1,
      "titles" : [
        "Melancholy III"
      ]
    },
    {
      "_id" : 300,
      "count" : 1,
      "titles" : [
        "Composition VII"
      ]
    },
    {
      // Includes document price outside of bucket boundaries, e.g., _id: 5
      "_id" : "Other",
      "count" : 1,
      "titles" : [
        "The Persistence of Memory"
      ]
    }
  ],
  "categorizedByTags" : [
    { "_id" : "painting", "count" : 6 },
    { "_id" : "oil", "count" : 4 },
    { "_id" : "Expressionism", "count" : 3 },
    { "_id" : "Surrealism", "count" : 2 },
    { "_id" : "abstract", "count" : 2 },
    { "_id" : "woodblock", "count" : 1 },
    { "_id" : "woodcut", "count" : 1 },
    { "_id" : "ukiyo-e", "count" : 1 },
    { "_id" : "satire", "count" : 1 },
    { "_id" : "caricature", "count" : 1 }
  ]
}
*/
```




