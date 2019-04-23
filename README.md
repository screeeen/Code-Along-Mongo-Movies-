# Code Along - Mongo DB


## Intro

![img](https://i.imgur.com/NzalR30.png)

When working with any Database, there are a few operations that we will always need to use. These operations are so popular that we have an acronym for it: CRUD stands for create, read, update and delete:

![img](https://i.imgur.com/CRowB2i.png)


## Getting Started

Using `mongoimport`, import the JSON data from the `movies.json` file into the collection `movies` in the `video` database.


```bash
# Run mongod
mongod

mongoimport --db video --collection movies --file movies.json --jsonArray
mongo
```


```js
use video

show collections
db.movies.find()
```


## Tasks


### 1. Retrieve all the documents  from the `movies` collection:

**<u>Your query</u>**:

```js

```

 

### 2. Retrieve all the documents  from the  `movies` collection and prettify the result:

**<u>Your query</u>**:

```js

```

 

### 3. Retrieve all the documents  from the  `movies` collection where the field `year` is  2000:

**<u>Your query</u>**:

```js
db.movies.find({ year: 2000}).pretty()
```

 

### 4. Retrieve all the documents from the `movies`  collection where the field `rate` is "8.8"

**<u>Your query</u>**:

```js
db.movies.find({ rate: "8.8"})
```

 

### 5. Retrieve the movie with the field `_id` "5cbc6943c95c41149fd2f3b5"

To specify an **ObjectID**, use the format **ObjectId(’id’)**, 

**<u>Your query</u>**:

```js
db.movies.find({_id: ObjectId("5cbf040626920f04b3dc2939")})
```

 

### 6.  Retrieve all documents in our collection where the field `year` equals `'2000'` **AND** the `rate` equals `'8.5'`.

**<u>Your query</u>**:

```js
db.movies.find({$and: [ {year: 2000},{rate:"8.5"}]}).pretty()
```

 

### 7. Retrieve all documents from the `movies` collection where the field `year` equals `2000` **OR** the `year` equals `2005`.

**<u>Your query</u>**:

```js
> db.movies.find({$or: [ {year: 2000},{year:2005}]}).pretty()
```

 

### 8. Retrieve all documents from the `movies` collection that do not have a rate of “9.0” and limit the result to 10 documents.

**<u>Your query</u>**:

```js
> db.movies.find({rate:{$ne:  "9.0"}}).limit(10)
```

 

### 9. Retrieve all documents from the `movies` collection where field `director` is `not` "Steven Spielberg" `or` "Quentin Tarantino".  

### Display only `title` and `director` fields for each document.

**<u>Your query</u>**:

```js
> db.movies.find({$nor:[{ director:'Steven Spielberg'},{director:'Quentin Tarantino'},{_id:0,name:1,title:0,director:0}]})
```

 

### 10. Retrieve all documents from the `movies` collection, using the projection return only the fields `title`, `year`, `genre` and exclude field `_id`.

**<u>Your query</u>**:

```js
> db.movies.find({},{_id:false,title:true,year:1,genre:1})
```

 

### 11. Retrieve all documents from the `movies` collection including only `title` field , using and sort them by `name` 

**<u>Your query</u>**:

```js
db.movies.find({},{_id:false,title:true}).sort({title:1})
```

 

### 12. Retrieve all documents from the `movies` collection including only `title`  and `director` fields ,  sort them by `name` , skipping first 5 documents

**<u>Your query</u>**:

```js
db.movies.find({},{_id:false,title:true,director:true}).sort({title:1}).skip(5)
```

 

### 13. Retrieve all documents from the `movies` collection where `director` field `equals`  "Robert Zemeckis"

**<u>Your query</u>**:

```js
db.movies.find({director:'Robert Zemeckis'})
```

 

### 14. Retrieve all documents from the `movies` collection where the `rate` field is different than "8.5". Using projection include only `title` and `rate` field, excluding `_id`

**<u>Your query</u>**:

```js
db.movies.find({rate:{$ne:  "8.5"}},{_id:0,title:1,rate:1})
```

 

### 15. Retrieve all documents from the `movies` collection where the `year` field is greater than or equal 2015. Using projection include only `title` , `year`and `director` fields.

**<u>Your query</u>**:

```js
db.movies.find({year:{$gte:2015}},{_id:0,title:1,year:1,director:1})
```

 

### 16. Retrieve all documents from the `movies` collection where the `year` field is less than 2000. Using projection include only `title` , `year`and `director` fields.

**<u>Your query</u>**:

```js
db.movies.find({year:{$lt:2000}},{_id:0,title:1,year:1,director:1})
```

 

### 17. Retrieve all documents from the `movies` collection created in the years 2000, 2005 and 2010. Sort the result by `year` in ascending order.

**<u>Your query</u>**:

```js
db.movies.find({year:{$in: [2000,2005,2010]}},{_id:0,year:1,title:1}).sort({year:1})
```

 

### 18. Retrieve all documents from the `movies` collection created in the years 1999 and 2010 and exluding the movie with `title` "Inception"

```js
db.movies.find({$and[{year: { $in [1999,2000]}},{title:{$ne:'Inception'}}],{title:1,year:1}
```



### 19. Delete documents from the `movies` collection created in the year 1999. 

**<u>Your query</u>**:

```js
db.movies.deleteMany({year:{$in: [1999]}})
```





### 20. Delete document from the `movies` collection with the `_id`  "5cbc6943c95c41149fd2f3bc".

 **<u>Your query</u>**:

```js
db.movies.deleteOne({_id: ObjectId("5cbc6943c95c41149fd2f3bc")})
```

 

### 21. Update all documents from the `movies` collection created in the `year` 2017 and add an additional named `rating`: 

```json
db.movies.updateMany({year:{$in: [2017]}})
```

###  

**<u>Your query</u>**:

```js
var ratingObj
{
	"rating" : "TV-G",
	"violence" : false,
	"drug_use" : false,
	"strong_language" : false
}

db.movies.updateMany({year:{$in:2017},{$set: { rating: ratingObj}})
```

 



### 22. Update the document from the `movies` collection with  `title` "Dunkirk" and set `rating`  to "PG-13" and fields  `violence` and `strong_language` to `true`  : 

### 

**<u>Your query</u>**:

```js
b.movies.updateOne( {title: 'Dunkirk'}, {$set:{ 'rating.rating':'PG.13', 'rating.violence':true, 'rating.strong_language':true}})
```

 



### 23. Delete documents from the `movies` collection using the titles provided in the array:

```js
let moviesToDelete = ["12 Angry Men", "Se7en", "Cidade de Deus", "Braveheart"]
```

###  

**<u>Your query</u>**:

```js
db.movies.deleteMany( { title:{ $in:["12 Angry Men", "Se7en", "Cidade de Deus", "Braveheart"] } } )
```

