# Adding More Fields

- If we try to get the author name from the server

```
{
  books {
    id
    author {
      name
    }
  }
}
```

- We will get error saying cannot query field "author"
- We will add a new field to our BookType object called author

```
const BookType = new GraphQLObjectType({
	name: 'Book',
	description: 'This represents a book written by an author',
	fields: () => ({
		id: { type: GraphQLNonNull(GraphQLInt) },
		name: { type: GraphQLNonNull(GraphQLString) },
		authorId: { type: GraphQLNonNull(GraphQLInt) }
		author: {
			type: AuthorType
			resolve: (book) => {
				return authors.find(author => author.id == book.authorid)
			}
		}
	})
})
```

- New author field is created with the type as `AuthorType`
- This will resolve to a function
- The function takes a parameter `book` 
- Now it returns the author
- It checks if the author id is equal to the book id or not
- Now create the AuthorType object

```
onst AuthorType = new GraphQLObjectType({
	name: 'Author',
	description: 'This represents an author of a book',
	fields: () => ({
		id: { type: GraphQLNonNull(GraphQLInt) },
		name: { type: GraphQLNonNull(GraphQLString) }
	})
})
```

- It will have the author id and the author name
- Now querying author name with id will give us the results

**query**

```
{
  books {
    id
    author {
      name
    }
  }
}
```

**output**

```
{
  "data": {
    "books": [
      {
        "id": 1,
        "author": {
          "name": "JK Rowling"
        }
      },
      {
        "id": 2,
        "author": {
          "name": "JK Rowling"
        }
      },
      {
        "id": 3,
        "author": {
          "name": "JK Rowling"
        }
      },
      {
        "id": 4,
        "author": {
          "name": "JRR Tokein"
        }
      },
      {
        "id": 5,
        "author": {
          "name": "JRR Tokein"
        }
      },
      {
        "id": 6,
        "author": {
          "name": "JRR Tokein"
        }
      },
      {
        "id": 7,
        "author": {
          "name": "Brent Weeks"
        }
      },
      {
        "id": 8,
        "author": {
          "name": "Brent Weeks"
        }
      }
    ]
  }
}
```

