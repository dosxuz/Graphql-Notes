# Adding Database to the Server

## Add name of some books

```js
const express = require('express')
const { graphqlHTTP } = require('express-graphql');

const {
        GraphQLSchema,
        GraphQLObjectType,
        GraphQLString
} = require('graphql')

const app = express()

const authors = [
        { id: 1, name: 'JK Rowling' },
        { id: 2, name: 'JRR Tokein' },
        { id: 3, name: 'Brent Weeks' }
]

const books = [
        { id:1, name: 'Harry Potter', authorid: 1 },
        { id:2, name: 'Some other shit', authorid: 1 },
        { id:3, name: 'Baaler chal', authorid: 1 },
        { id:4, name: 'Boi er naam', authorid: 2 },
        { id:5, name: 'Chudir bhai', authorid: 2 },
        { id:6, name: 'chondro gupto', authorid: 2 },
        { id:7, name: 'Pod mere', authorid: 3 },
        { id:8, name: 'Gondo shukto', authorid: 3 }
]

const schema = new GraphQLSchema({
        query: new GraphQLObjectType({
                name: 'HelloWorld',
                fields: () => ({
                        message: { 
                                type: GraphQLString,
                                resolve: () => 'Hello World'
                        }
                })
        })
})

app.use('/graphql', graphqlHTTP({
        schema: schema,
        graphiql: true
}))

app.listen(5000., () => console.log('Server Running'))
```

## Adding a Root Query Section 

- Right now we can only query the hello world object from the messages field

```
const express = require('express')
const { graphqlHTTP } = require('express-graphql');

const {
	GraphQLSchema,
	GraphQLObjectType,
	GraphQLString,
	GraphQLList,
	GraphQLInt,
	GraphQLNonNUll
} = require('graphql')

const app = express()

const authors = [
	{ id: 1, name: 'JK Rowling' },
	{ id: 2, name: 'JRR Tokein' },
	{ id: 3, name: 'Brent Weeks' }
]

const books = [
	{ id:1, name: 'Harry Potter', authorid: 1 },
	{ id:2, name: 'Some other shit', authorid: 1 },
	{ id:3, name: 'Baaler chal', authorid: 1 },
	{ id:4, name: 'Boi er naam', authorid: 2 },
	{ id:5, name: 'Chudir bhai', authorid: 2 },
	{ id:6, name: 'chondro gupto', authorid: 2 },
	{ id:7, name: 'Pod mere', authorid: 3 },
	{ id:8, name: 'Gondo shukto', authorid: 3 }
]

const BookType = new GraphQLObjectType({
	name: 'Book',
	description: 'This represents a book written by an author',
	fields: () => ({
		id: { type: GraphQLNonNull(GraphQLInt) },
		name: { type: GraphQLNonNull(GraphQLString) },
		authorId: { type: GraphQLNonNull(GraphQLInt) }
	})
})

const RootQueryTpye = new GraphQLObjectType ({
	name: 'Query',
	description: 'Root Query',
	fields: () => ({
		books: {
			type: new GraphQLList(BookType),
			description: 'List of Books',
			resolve: () => books
		})
	})
})


app.use('/graphql', graphqlHTTP({
	schema: schema,
	graphiql: true
}))

app.listen(5000., () => console.log('Server Running'))
```

- The root query creates the basic structure for our query

```
const RootQueryTpye = new GraphQLObjectType ({
	name: 'Query',
	description: 'Root Query',
	fields: () => ({
		books: {
			type: new GraphQLList(BookType),
			description: 'List of Books',
			resolve: () => books
		})
	})
})
```

- This will define the BooType object

```js
const BookType = new GraphQLObjectType({
	name: 'Book',
	description: 'This represents a book written by an author',
	fields: () => ({
		id: { type: GraphQLNonNull(GraphQLInt) },
		name: { type: GraphQLNonNull(GraphQLString) },
		authorId: { type: GraphQLNonNull(GraphQLInt) }
	})
})
```

- Using `({})`	as the body of the function will return whatever is the result of the function
- The parameters `id, name, authorId` will directly fetch from the database, as there are names of the type
- Datatype `GraphQLNotNull` is used, so that it does not take a null value
- Schema has to be added

```js
const schema = new GraphQLSchema ({
        query: RootQueryType
})
```

- The schema will query the `RootQueryType`

**server.js**

```js
const express = require('express')
const { graphqlHTTP } = require('express-graphql');

const {
	GraphQLSchema,
	GraphQLObjectType,
	GraphQLString,
	GraphQLList,
	GraphQLInt,
	GraphQLNonNull
} = require('graphql')

const app = express()

const authors = [
	{ id: 1, name: 'JK Rowling' },
	{ id: 2, name: 'JRR Tokein' },
	{ id: 3, name: 'Brent Weeks' }
]

const books = [
	{ id:1, name: 'Harry Potter', authorid: 1 },
	{ id:2, name: 'Some other shit', authorid: 1 },
	{ id:3, name: 'Baaler chal', authorid: 1 },
	{ id:4, name: 'Boi er naam', authorid: 2 },
	{ id:5, name: 'Chudir bhai', authorid: 2 },
	{ id:6, name: 'chondro gupto', authorid: 2 },
	{ id:7, name: 'Pod mere', authorid: 3 },
	{ id:8, name: 'Gondo shukto', authorid: 3 }
]

const BookType = new GraphQLObjectType({
	name: 'Book',
	description: 'This represents a book written by an author',
	fields: () => ({
		id: { type: GraphQLNonNull(GraphQLInt) },
		name: { type: GraphQLNonNull(GraphQLString) },
		authorId: { type: GraphQLNonNull(GraphQLInt) }
	})
})

const RootQueryType = new GraphQLObjectType ({
	name: 'Query',
	description: 'Root Query',
	fields: () => ({
		books: {
			type: new GraphQLList(BookType),
			description: 'List of Books',
			resolve: () => books
		}
	})
})

const schema = new GraphQLSchema ({
	query: RootQueryType
})


app.use('/graphql', graphqlHTTP({
	schema: schema,
	graphiql: true
}))

app.listen(5000., () => console.log('Server Running'))
```

- Refreshing the server will give us the documentation explorer containing the different query type

## Sending Queries

- Get the names of all books

```
{
  books {
    name
  }
}
```

**Output**

```
{
  "data": {
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
}
```

- Get the id and names of all books

**query**

```
{
  books {
    id
    name
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
      }
    ]
  }
}
```

- Get only the id 

**query**

```
{
  books {
    id
  }
}
```

**output**

```
{
  "data": {
    "books": [
      {
        "id": 1
      },
      {
        "id": 2
      },
      {
        "id": 3
      },
      {
        "id": 4
      },
      {
        "id": 5
      },
      {
        "id": 6
      },
      {
        "id": 7
      },
      {
        "id": 8
      }
    ]
  }
}
```

