# Data Normalization

### Questions

* what is the redux store?
* why is it important to keep the store organized?
* how do we organize our store in the most efficient way?

### Problems with non-normalized data
* When a piece of data is duplicated in several places, it becomes harder to make sure that it is updated appropriately.
* Nested data means that the corresponding reducer logic has to be more nested or more complex. In particular, trying to update a deeply nested field can become very ugly very fast.  
* Since immutable data updates require all ancestors in the state tree to be copied and updated as well, and new object references will cause connected UI components to re-render, an update to a deeply nested data object could force totally unrelated UI components to re-render even if the data they're displaying hasn't actually changed.

## Normalizing Data

### Overview

* technique for data storage in Redux store
* flattening, simplified reducer logic
* avoids duplicating data
* dynamic updating
* change propagation
* denormalize in mapStateToProps

### Guidelines

* Each type of data gets its own "table" in the state.
* Each "data table" should store the individual items in an object, with the IDs of the items as keys and the items themselves as the values.
* Any references to individual items should be done by storing the item's ID.
* Arrays of IDs should be used to indicate ordering.

### Caveats

* javascript objects are not ordered
* store lists as just IDs and iterate later

"To maintain the order of data from the API you must iterate through the result property of the normalized object. This is an array which lists the IDs of entities from the search result. And arrays safely guarantee the order of its values.

If you're iterating through an embedded resource normalizr replaces these with an array of IDs also in the same order as the API." - tonyhb

```javascript
{
  users : {
    byId : {
      "user1" : {
        username : "user1",
        name : "User 1",
      }
      "user2" : {
        username : "user2",
        name : "User 2",
      }
      "user3" : {
        username : "user3",
        name : "User 3",
      }
    },
    allIds : ["user1", "user2", "user3"]
  }
}
```

## Examples

### Non-Normalized
```javascript
state = {
  posts: [{
    title: "Redux mistakes",
    author: {
      name: "Matt Zeunert"
    }
  }]
}

name = post.author.name
```

### Normalized
```javascript
state = {
  posts: {
    10: {
      id: 10
      title: "Redux Mistakes"
      author: {id: 50}
    }
  },
  users: {
    50: {
      id: 50,
      name: "Matt Zeunert"
    }
  }
}

name = users[post.author.id].name
```

## Normalizr

* takes JSON with a schema definition
* returns nested entities with IDs
* gathers in dictionaries

### Original Data

```json
{
  "id": "123",
  "author": {
    "id": "1",
    "name": "Paul"
  },
  "title": "My awesome blog post",
  "comments": [
    {
      "id": "324",
      "commenter": {
        "id": "2",
        "name": "Nicole"
      }
    }
  ]
}
```

### Using the API

```javascript
import { normalize, schema } from 'normalizr';

// Define a users schema
const user = new schema.Entity('users');

// Define your comments schema
const comment = new schema.Entity('comments', {
  commenter: user
});

// Define your article
const article = new schema.Entity('articles', {
  author: user,
  comments: [ comment ]
});

const normalizedData = normalize(originalData, article);
```

### Normalized Data

```javascript
{
  result: "123",
  entities: {
    "articles": {
      "123": {
        id: "123",
        author: "1",
        title: "My awesome blog post",
        comments: [ "324" ]
      }
    },
    "users": {
      "1": { "id": "1", "name": "Paul" },
      "2": { "id": "2", "name": "Nicole" }
    },
    "comments": {
      "324": { id: "324", "commenter": "2" }
    }
  }
}
```

## References and More Info

* https://egghead.io/lessons/javascript-redux-normalizing-the-state-shape
* https://tonyhb.gitbooks.io/redux-without-profanity/content/normalizer.html
* http://redux.js.org/docs/recipes/reducers/NormalizingStateShape.html
* http://redux.js.org/docs/recipes/reducers/UpdatingNormalizedData.html
* https://github.com/paularmstrong/normalizr
