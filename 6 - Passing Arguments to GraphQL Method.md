# Passing Argument to GraphQL Method

```
const RootQueryType = new GraphQLObjectType ({
	name: 'Query',
	description: 'Root Query',
	fields: () => ({
		book: {
			type: BookType,
			description: 'A single book',
			args: {
				id: { type: GraphQLInt }
			},
			resolve: (parent, args) => books.find(book => book.id == args.id)
		},
		books: {
			type: new GraphQLList(BookType),
			description: 'List of Books',
			resolve: () => books
		},
		authors: {
			type: GraphQLList(AuthorType),
			description: 'List of all Authors',
			resolve: () => authors
		}
```

- Add one field for a single book
- Add the type as BookType and not GraphQLList type
- The resolve function takes two arguments, (parent) which we don't need and (args)
- The `args` parameter is defined as the id of the book which is a GraphQLInt
- The resolve() function will find the book.id which matches with the queried book id
- Now we can query a single book with the id

**query**

```
{
  book(id: 1) {
    name
  }
}
```


**output**

```
{
  "data": {
    "book": {
      "name": "Harry Potter"
    }
  }
}
```

- Also get the author of the book

**query**

```
{
  book(id: 1) {
    name
    author{
      name
    }
  }
}
```

**output**

```
{
  "data": {
    "book": {
      "name": "Harry Potter",
      "author": {
        "name": "JK Rowling"
      }
    }
  }
}
```

## Getting a single author

```
const RootQueryType = new GraphQLObjectType ({
	name: 'Query',
	description: 'Root Query',
	fields: () => ({
		book: {
			type: BookType,
			description: 'A single book',
			args: {
				id: { type: GraphQLInt }
			},
			resolve: (parent, args) => books.find(book => book.id == args.id)
		},
		books: {
			type: new GraphQLList(BookType),
			description: 'List of Books',
			resolve: () => books
		},
		authors: {
			type: GraphQLList(AuthorType),
			description: 'List of all Authors',
			resolve: () => authors
		},

		author: {
			type: AuthorType,
			description: 'A single author',
			args: {
				id: { type: GraphQLInt }
			},
			resolve: (parent, args) => authors.find(author => author.id === args.id)
		}
	})
})
```

- Add a field author
- It will take the id of the author as `GraphQLInt`
- It will match with the author.id in the list with the author id passed `args.id`
- We can get a single author using author id

**query**

```
{
  author(id: 2) {
    name
  }
}
```

**output**

```
{
  "data": {
    "author": {
      "name": "JRR Tokein"
    }
  }
}
```

- Field is returning a function that returns an object
- Everything is defined in a function so that they can reference each other before they are defined

