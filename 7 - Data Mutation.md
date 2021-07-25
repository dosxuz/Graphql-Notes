# Data Mutation

- Mutation is GraphQL version of using POST, PUT and DELETE on a REST API server
- Mutations create changes to the existing data

## Updating the schema

- The schema takes a mutation field

```
const schema = new GraphQLSchema ({
        query: RootQueryType,
        mutation: RootMutationType
})
```

- The schema will have a mutation with the type `RootMutationType` which we will create

```
const RootMutationType = new GraphQLObjectType ({
        name: 'Mutation',
        description: 'Root Mutation',
        fields: () => ({
                addBook: {
                        type: BookType,
                        description: 'Add a book',
                        args: { 
                                name: { type: GraphQLNonNull(GraphQLString) },
                                authorid: { type: GraphQLNonNull(GraphQLInt) }
                        },
                        resolve: (parent, args) => {
                                const book = { id: books.length + 1, name: args.name, authorid: args.authorid }
                                books.push(book)
                                return book
                        }
                }
        })
})
```

- The mutation type will take a book name and the authorid from the argument and the book id will be one more than the length of the book lists length
- Then will push the book object to the array
- It will also return the book object, since the mutation function returns a `BookType` object
- Add and query the name of the added book

**query**

```
mutation {
  addBook(name: "Fifty shades of chodon", authorid: 4) {
  	id
    name
  }
}
```

**output**

```
{
  "data": {
    "addBook": {
      "id": 9,
      "name": "Fifty shades of chodon"
    }
  }
}
```

- Check the book is added

```
{
  books {
    id
    name
  }
}
```

```
{
  "data": {
    "books": [
      {
        "id": 1,
        "name": "Harry Potter"
      },
      {
        "id": 2,
        "name": "Some other shit"
      },
      {
        "id": 3,
        "name": "Baaler chal"
      },
      {
        "id": 4,
        "name": "Boi er naam"
      },
      {
        "id": 5,
        "name": "Chudir bhai"
      },
      {
        "id": 6,
        "name": "chondro gupto"
      },
      {
        "id": 7,
        "name": "Pod mere"
      },
      {
        "id": 8,
        "name": "Gondo shukto"
      },
      {
        "id": 9,
        "name": "Fifty shades of chodon"
      }
    ]
  }
}
```


## Adding author

- Add new mutation `addAuthor` 

```
const RootMutationType = new GraphQLObjectType ({
        name: 'Mutation',
        description: 'Root Mutation',
        fields: () => ({
                addBook: {
                        type: BookType,
                        description: 'Add a book',
                        args: { 
                                name: { type: GraphQLNonNull(GraphQLString) },
                                authorid: { type: GraphQLNonNull(GraphQLInt) }
                        },
                        resolve: (parent, args) => {
                                const book = { id: books.length + 1, name: args.name, authorid: args.authorid }
                                books.push(book)
                                return book
                        }
                },

                addAuthor: {
                        type: AuthorType,
                        description: 'Add an author',
                        args: { 
                                name: { type: GraphQLNonNull(GraphQLString) }
                        },
                        resolve: (parent, args) => {
                                const author = { id: authors.length + 1, name: args.name }
                                authors.push(author)
                                return author
                        }
                }

        })
})
```

- It takes the author name as argument
- Then the id is added as one more than the lenght of the array
- The name is added from the argument
- The author type object is then pushed to the array
- Then the author return type is returned

- Add an author and query its id and name

**query**

```
mutation {
  addAuthor(name:"Chodon Churdhuri") {
    id
    name
  }
}
```

**output**

```
{
  "data": {
    "addAuthor": {
      "id": 4,
      "name": "Chodon Churdhuri"
    }
  }
}
```

- Check if the author is added

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
      },
      {
        "id": 4,
        "name": "Chodon Churdhuri",
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

