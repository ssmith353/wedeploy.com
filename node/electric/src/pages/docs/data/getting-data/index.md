---
title: "Getting Data"
description: "Get an existing field, document or collection in the database."
headerTitle: "Data"
layout: "guide"
weight: 4
---

### {$page.title}

###### {$page.description}

<aside>

If you are unfamiliar with our API, please visit the [WeDeploy SDK's](/docs/configure/wedeploy-sdks/) page first to learn how to install and configure it.

</aside>

<article id="1">

## Get Collection

It is simple and easy to start getting documents from your saved data collections. You simply use the `get` method in your WeDeploy API call and then pass the name of the collection you want to retrieve.

```javascript
WeDeploy
  .data('https://<serviceID>-<projectID>.wedeploy.io')
  .get('movies')
  .then(function(movie) {
    console.log(movie);
  });
```
```swift
WeDeploy
  .data('https://<serviceID>-<projectID>.wedeploy.io')
  .get(resourcePath: "movies")
  .then { movie in
    print(movie)
  }
```
```text/x-java
WeDeploy
  .data("https://<serviceID>-<projectID>.wedeploy.io")
  .get("movies")
  .execute();
```
```text/x-sh
curl -X "GET" "https://<serviceID>-<projectID>.wedeploy.io/movies" \
     -H 'Authorization: Bearer <your-project-master-token>' \
```

The response will give you all the documents inside that collection.

```javascript
[
  {"id":"star_wars_i", "title":"Star Wars: Episode I - The Phantom Menace", "year":1999, "rating":6.5},
  {"id":"star_wars_ii", "title":"Star Wars: Episode II - Attack of the Clones", "year":2002, "rating":6.7},
  {"id":"star_wars_iii", "title":"Star Wars: Episode III - Revenge of the Sith", "year":2005, "rating":7.7},
  {"id":"star_wars_iv", "title":"Star Wars: Episode IV - A New Hope", "year":1977, "rating":8.7},
  {"id":"star_wars_v", "title":"Star Wars: Episode V - The Empire Strikes Back", "year":1980, "rating":8.8},
  {"id":"star_wars_vi", "title":"Star Wars: Episode VI - Return of the Jedi", "year":1983, "rating":8.4},
  {"id":"star_wars_vii", "title":"Star Wars: Episode VII - The Force Awakens", "year":2015}
]
```

</article>

<article id="2">

## Get with Data Path

We can also get any document body or document field value using the full data path (`collection/documentId/documentField`):

```javascript
WeDeploy
  .data('https://<serviceID>-<projectID>.wedeploy.io')
  .get('movies/star_wars_v/title')
  .then(function(title) {
    console.log(title);
  });
```
```swift
WeDeploy
  .data('https://<serviceID>-<projectID>.wedeploy.io')
  .get(resourcePath: "movies/star_wars_v/title")
  .then { (movie: String) in // You have to specify the type here to allow compiler infer type
    print(movie)
  }
```
```text/x-java
WeDeploy
  .data('https://<serviceID>-<projectID>.wedeploy.io')
  .get("movies/star_wars_v/title")
  .execute();
```
```text/x-sh
curl -X "GET" "https://<serviceID>-<projectID>.wedeploy.io/movies/star_wars_v/title" \
     -H 'Authorization: Bearer <your-project-master-token>' \
```

</article>

<article id="3">

## Sorting and Filtering

When you request to get a collection, all the documents inside that collection will be sent to you ordered by the date they were created (`createdAt`). So what if you want to filter or sort your results?

**Sorting**

Below you can see an example of sorting the results from your request in descending order based on the rating field.

```javascript
WeDeploy
  .data('https://<serviceID>-<projectID>.wedeploy.io')
  .orderBy('rating', 'desc')
  .get('movies')
  .then(function(movies) {
    console.log(movies);
  });
```
```swift
WeDeploy
  .data('https://<serviceID>-<projectID>.wedeploy.io')
  .orderBy(field: "rating", order: .DESC)
  .get(resourcePath: "movies")
  .then { movies in
    print(movies)
  }
```
```text/x-java
WeDeploy
  .data("https://<serviceID>-<projectID>.wedeploy.io")
  .orderBy("rating", SortOrder.DESCENDING)
  .get("movies")
  .execute();
```
```text/x-sh
curl -X "POST" "https://<serviceID>-<projectID>.wedeploy.io/movies" \
     -H 'Content-Type: application/json' \
     -H 'Authorization: Bearer <your-project-master-token>' \
     -d $'{
        "sort": [
          {
            "rating": "desc"
          }
        ]
      }'
```

The result would be the following list if documents sorted by rating.

```javascript
[
  {"id":"star_wars_v","title":"Star Wars: Episode V - The Empire Strikes Back","year":1980,"rating":8.8},
  {"id":"star_wars_iv","title":"Star Wars: Episode IV - A New Hope","year":1977,"rating":8.7},
  {"id":"star_wars_vi","title":"Star Wars: Episode VI - Return of the Jedi","year":1983,"rating":8.4},
  {"id":"star_wars_iii","title":"Star Wars: Episode III - Revenge of the Sith","year":2005,"rating":7.7},
  {"id":"star_wars_ii","title":"Star Wars: Episode II - Attack of the Clones","year":2002,"rating":6.7},
  {"id":"star_wars_i","title":"Star Wars: Episode I - The Phantom Menace","year":1999,"rating":6.5},
  {"id":"star_wars_vii","title":"Star Wars: Episode VII - The Force Awakens","year":2015}
]
```

**Filtering**

You can also provide filters so that only documents that match your query will be returned in the result.

```javascript
WeDeploy
  .data('https://<serviceID>-<projectID>.wedeploy.io')
  .where('year', '<', 2000)
  .or('rating', '>', 8.5)
  .get('movies')
  .then(function(movies) {
    console.log(movies);
  });
```
```swift
WeDeploy
  .data('https://<serviceID>-<projectID>.wedeploy.io')
  .where(field: "year", op: "<", value: 2000)
  .or(field: "rating", op: ">", value: 8.5)
  .get(resourcePath: "movies")
  .then { movies in
    print(movies)
  }
```
```text/x-java
WeDeploy
  .data("https://<serviceID>-<projectID>.wedeploy.io")
  .where(lt("year", 2000).or(gt("rating", 8.5)))
  .get("movies")
  .execute();
```
```text/x-sh
curl -X "POST" "https://<serviceID>-<projectID>.wedeploy.io/movies" \
     -H 'Content-Type: application/json' \
     -H 'Authorization: Bearer <your-project-master-token>' \
     -d $'{
        "filter": [
          {
            "or": [
              {
                "year": {
                  "value": 2000,
                  "operator": "<"
                }
              },
              {
                "rating": {
                  "value": 8.5,
                  "operator": ">"
                }
              }
            ]
          }
        ]
      }'
```

The result will be any documents from that collection that match these filter parameters.

```javascript
[
  {"id":"star_wars_iv","title":"Star Wars: Episode IV - A New Hope","year":1977,"rating":8.7},
  {"id":"star_wars_v","title":"Star Wars: Episode V - The Empire Strikes Back","year":1980,"rating":8.8}
]
```

<aside>

For more examples of useful filters and result sorting you can use, see our **[Filtering Data page](/docs/data/filtering-data/)**.

</aside>

</article>

## What's next?

Now that you've learned how to retrieve, you can start [using real-time](/docs/data/real-time-data/).
