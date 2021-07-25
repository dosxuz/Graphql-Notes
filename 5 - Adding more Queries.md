# Adding More Queries

## Adding Query for Getting Authors

- Add a new query along with the book query

```js
const RootQueryType = new GraphQLObjectType ({
        name: 'Query',
        description: 'Root Query',
        fields: () => ({
                books: {
                        type: new GraphQLList(BookType),
                        description: 'List of Books',
                        resolve: () => books
                },
                author: {
                        type: GraphQLList(AuthorType),
                        description: 'List of all Authors',
                        resolve: () => authors
                }
        })
})
```

- Now we can  query the authors name 

**query**

```
{
 authors {
  name
}
}
```

**output**

```
{
  "data": {
    "authors": [
      {
        "name": "JK Rowling"
      },
      {
        "name": "JRR Tokein"
      },
      {
        "name": "Brent Weeks"
      }
    ]
  }
}
```


## Adding books field for author

- If we query books under authors, we won't get result
- We need to get list of books with the author name

```
const AuthorType = new GraphQLObjectType({
	name: 'Author',
	description: 'This represents an author of a book',
	fields: () => ({
		id: { type: GraphQLNonNull(GraphQLInt) },
		name: { type: GraphQLNonNull(GraphQLString) },
		books: { 
			type: new GraphQLList(BookType),
			resolve: (author) => {
				return books.filter(book => books.id == authors.id)
			}
		}
	})
})
```

- This books field will be of type `GraphQLList` 
- It will take `author` as the parent parameter
- Then it will resolve a function 
- This function will filter by matching the book.id with the authors.id
- Now we can query the author name with a list of books written by that author

**query**

```
{
  authors {
    id
    name
    books {
      name
    }
  }
}
```

**output**

```
{
  "data": {
    "authors": [
      {
        "id": 1,
        "name": "JK Rowling",
        "books": [
          {
            "name": "Harry Potter"
          },
          {
            "name": "Some other shit"
          },
          {
            "name": "Baaler chal"
          },
          {
            "name": "Boi er naam"
          },
          {
            "name": "Chudir bhai"
          },
          {
            "name": "chondro gupto"
          },
          {
            "name": "Pod mere"
          },
          {
            "name": "Gondo shukto"
          }
        ]
      },
      {
        "id": 2,
        "name": "JRR Tokein",
        "books": [
          {
            "name": "Harry Potter"
          },
          {
            "name": "Some other shit"
          },
          {
            "name": "Baaler chal"
          },
          {
            "name": "Boi er naam"
          },
          {
            "name": "Chudir bhai"
          },
          {
            "name": "chondro gupto"
          },
          {
            "name": "Pod mere"
          },
          {
            "name": "Gondo shukto"
          }
        ]
      },
      {
        "id": 3,
        "name": "Brent Weeks",
        "books": [
          {
            "name": "Harry Potter"
          },
          {
            "name": "Some other shit"
          },
          {
            "name": "Baaler chal"
          },
          {
            "name": "Boi er naam"
          },
          {
            "name": "Chudir bhai"
          },
          {
            "name": "chondro gupto"
          },
          {
            "name": "Pod mere"
          },
          {
            "name": "Gondo shukto"
          }
        ]
      }
    ]
  }
}
```

