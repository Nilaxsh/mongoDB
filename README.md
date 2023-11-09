**1. Create a Database called movies.**
```
use movies
switched to db movies
```
**2. Create a collection called movie details.**
```
db.createCollections("moviedetails")
{ok:1}
```
**3. Create above 5 movie documents into a movie details collection.**
```
db.moviedetails.insertMany([{"Movie-Title":"Jurassic Park","Genre/Type":"Adventure","Director":"Stevespielberg","Release Year":1993},{"Movie-Title":"Forrest Gump","Genre/Type":"Drama","Director":"Robert Zemeckies","Release Year":1994},{"Movie-Title":"Titanic","Genre/Type":"Romance","Director":"James Cameron","Release Year":1997},{"Movie-Title":"The Dark Knight","Genre/Type":"Action","Director":"Christopher Nolan","Release Year":2008},{"Movie-Title":"Avatar","Genre/Type":"Science Fiction","Director":"James Cameron","Release Year":2009}])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("654c84c522c09d01135451e3"),
    '1': ObjectId("654c84c522c09d01135451e4"),
    '2': ObjectId("654c84c522c09d01135451e5"),
    '3': ObjectId("654c84c522c09d01135451e6"),
    '4': ObjectId("654c84c522c09d01135451e7")
  }
}
```

**4. List all documents created.**
```
movies> db.moviedetails.find()
[
  {
    _id: ObjectId("654c84c522c09d01135451e3"),
    'Movie-Title': 'Jurassic Park',
    'Genre/Type': 'Adventure',
    Director: 'Stevespielberg',
    'Release Year': 1993
  },
  {
    _id: ObjectId("654c84c522c09d01135451e4"),
    'Movie-Title': 'Forrest Gump',
    'Genre/Type': 'Drama',
    Director: 'Robert Zemeckies',
    'Release Year': 1994
  },
  {
    _id: ObjectId("654c84c522c09d01135451e5"),
    'Movie-Title': 'Titanic',
    'Genre/Type': 'Romance',
    Director: 'James Cameron',
    'Release Year': 1997
  },
  {
    _id: ObjectId("654c84c522c09d01135451e6"),
    'Movie-Title': 'The Dark Knight',
    'Genre/Type': 'Action',
    Director: 'Christopher Nolan',
    'Release Year': 2008
  },
  {
    _id: ObjectId("654c84c522c09d01135451e7"),
    'Movie-Title': 'Avatar',
    'Genre/Type': 'Science Fiction',
    Director: 'James Cameron',
    'Release Year': 2009
  }
]
movies> db.moviedetails.find({"Director":"James Cameron"})
[
  {
    _id: ObjectId("654c84c522c09d01135451e5"),
    'Movie-Title': 'Titanic',
    'Genre/Type': 'Romance',
    Director: 'James Cameron',
    'Release Year': 1997
  },
  {
    _id: ObjectId("654c84c522c09d01135451e7"),
    'Movie-Title': 'Avatar',
    'Genre/Type': 'Science Fiction',
    Director: 'James Cameron',
    'Release Year': 2009
  }
]
```

**5.List James Cameron’s movies.**
```
db.moviedetails.find({"Director":"James Cameron"},{"Genre/Type":0,"Release Year":0,_id:0})
[
  { 'Movie-Title': 'Titanic', Director: 'James Cameron' },
  { 'Movie-Title': 'Avatar', Director: 'James Cameron' }
]
```

**6.List  James Cameron’s movies released in 2009.**
```
db.moviedetails.find({"Release Year":2009})
[
  {
    _id: ObjectId("654c84c522c09d01135451e7"),
    'Movie-Title': 'Avatar',
    'Genre/Type': 'Science Fiction',
    Director: 'James Cameron',
    'Release Year': 2009
  }
]
```
**7.Delete the movie which you don’t like.**
```
db.moviedetails.remove({"Movie-Title":"Avatar"})
DeprecationWarning: Collection.remove() is deprecated. Use deleteOne, deleteMany, findOneAndDelete, or bulkWrite.
{ acknowledged: true, deletedCount: 1 }
movies> db.moviedetails.find()
[
  {
    _id: ObjectId("654c84c522c09d01135451e3"),
    'Movie-Title': 'Jurassic Park',
    'Genre/Type': 'Adventure',
    Director: 'Stevespielberg',
    'Release Year': 1993
  },
  {
    _id: ObjectId("654c84c522c09d01135451e4"),
    'Movie-Title': 'Forrest Gump',
    'Genre/Type': 'Drama',
    Director: 'Robert Zemeckies',
    'Release Year': 1994
  },
  {
    _id: ObjectId("654c84c522c09d01135451e5"),
    'Movie-Title': 'Titanic',
    'Genre/Type': 'Romance',
    Director: 'James Cameron',
    'Release Year': 1997
  },
  {
    _id: ObjectId("654c84c522c09d01135451e6"),
    'Movie-Title': 'The Dark Knight',
    'Genre/Type': 'Action',
    Director: 'Christopher Nolan',
    'Release Year': 2008
  }
]
```
**Add the movie which is your favourite.** 
```
db.moviedetails.insertOne({"Movie-Title":"Leo","Genre/Type":"Action","Director":"logesh","Release Year":2024})

{
  acknowledged: true,
  insertedId: ObjectId("654c97dd22c09d01135451e8")
}
movies> db.moviedetails.find()
[
  {
    _id: ObjectId("654c84c522c09d01135451e3"),
    'Movie-Title': 'Jurassic Park',
    'Genre/Type': 'Adventure',
    Director: 'Stevespielberg',
    'Release Year': 1993
  },
  {
    _id: ObjectId("654c84c522c09d01135451e4"),
    'Movie-Title': 'Forrest Gump',
    'Genre/Type': 'Drama',
    Director: 'Robert Zemeckies',
    'Release Year': 1994
  },
  {
    _id: ObjectId("654c84c522c09d01135451e5"),
    'Movie-Title': 'Titanic',
    'Genre/Type': 'Romance',
    Director: 'James Cameron',
    'Release Year': 1997
  },
  {
    _id: ObjectId("654c84c522c09d01135451e6"),
    'Movie-Title': 'The Dark Knight',
    'Genre/Type': 'Action',
    Director: 'Christopher Nolan',
    'Release Year': 2008
  },
  {
    _id: ObjectId("654c97dd22c09d01135451e8"),
    'Movie-Title': 'Leo',
    'Genre/Type': 'Action',
    Director: 'logesh',
    'Release Year': 2024
  }
]
```

**9.List movie Directed  by Christopher Nolan in 1994.**
```
db.moviedetails.find({"Director":"christopher","Release Year":1994})
Empty file
```
**10.List out the Director’s Name in your document.**
```
movies> db.moviedetails.distinct("Director")
[
  'Christopher Nolan',
  'James Cameron',
  'Robert Zemeckies',
  'Stevespielberg',
  'logesh'
]
```

