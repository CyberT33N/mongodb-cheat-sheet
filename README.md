# MongoDB Cheat Sheet
MongoDB Cheat Sheet with the most needed stuff..

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

var collection = MongoDB.collection('import');
collection.find( {"used": 0} ).limit( 1 ).toArray(function(e, docs) {


    if(e){
       log( chalk.red.bold('❌ ERROR') + ' There was an error while try to get the current page - ' + chalk.white.bold('error:\n') + e );
       //assert.equal(null, e);
       return;
     } 


        if( docs[0] ){
        log( 'Found the following records:\n' + JSON.stringify(docs, null, 4) );
        log( chalk.green.bold('✔ SUCCESS') + ' LISTING AREA - We successfully get the current import from MongoDB:\n' + chalk.white.bold( docs[0].url ) );

           t33n.url = docs[0].url;
           log( 'current import url:' + t33n.url );

        } 
        else{

          log(`It seems that we used now all data from the DB. Everything was marked as used..
          ############ FINISH ##############`);

        } 



}); 


```










## find object id
```javascript
var ObjectId = require('mongodb').ObjectId;
var id = "5f2a40a54d054559dcc566ff";
var o_id = new ObjectId(id);

let collection = MongoDB.collection('export');
collection.find( {"itemdetails._id":o_id} ).toArray(function(e, docs) { });
```




## find specific data
Notice that it will returns an array with all results based on your search value. 
```javascript
// sync
collection.find( {"token": token} ).toArray(function(e, docs) { //.. });

// async
const verify = await collection.find( {"token": token} ).toArray({});
```


## find random document with used = 0 and limit to 1 item
```javascript
collection.aggregate([ { $match: { used: 0 } }, { $sample: { size: 1 } } ]).toArray(function(e, docs) {  });
```







<br />
<br />


 _____________________________________________________
 _____________________________________________________


<br />
<br />


# Update


## update field in collection
```javascript

var query = { url: t33n.url };
var newvalues = { $set: { used: 1 } };


var collection = MongoDB.collection('import');
collection.updateOne(query, newvalues, function(e, res) { //.. });

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
collection.insertOne(json, function(e, result) { //.. });

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
collection.deleteOne({"id": json.id}, function(e, result) { //.. });

//async
const r = await collection.deleteOne( {"id": json.id} );
```




