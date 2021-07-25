# Setting up GraphQL

- Use npm to create package json file

```
npm init
```

- Change the package.json as follows

```json
cat package.json 
{
  "name": "practice",
  "version": "1.0.0",
  "description": "",
  "main": "server.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

- Install all the dependencies needed

```
npm i express express-graphql graphql
```

- Install nodemon as dev dependency

```
npm i --save-dev nodemon
```

- Add a script in package.json

```
{
  "name": "practice",
  "version": "1.0.0",
  "description": "",
  "main": "server.js",
  "scripts": {
    "devStart": "nodemon server.js"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1",
    "express-graphql": "^0.12.0",
    "graphql": "^15.5.1"
  },
  "devDependencies": {
    "nodemon": "^2.0.12"
  }
}
```

## Create the server file

**server.js**

```js
const express = require('express')
const app = express()
app.listen(5000., () => console.log('Server Running'))
```

- Run the server as 

```
npm run devStart
```

- This will run our server on localhost port 5000

## Adding GraphQL to our server

```js
const express = require('express')
const { graphqlHTTP } = require('express-graphql');

const app = express()

app.use('/graphql', graphqlHTTP({
        graphiql: true
}))

app.listen(5000., () => console.log('Server Running'))
```

- Going to the url `/graphql` will tell us, it needs a schema
- Define a schema, which tells how all of our data is interacted

## Creating a schema

### Add Graphql Object type

```
const express = require('express')
const { graphqlHTTP } = require('express-graphql');

const {
        GraphQLSchema,
        GraphQLObjectType
} = require('graphql')

const app = express()

app.use('/graphql', graphqlHTTP({
        graphiql: true
}))

app.listen(5000., () => console.log('Server Running'))
```

### Adding the schema

- We will create a dummy schema
- The first section will have getting of data

```js
const express = require('express')
const { graphqlHTTP } = require('express-graphql');

const {
        GraphQLSchema,
        GraphQLObjectType,
        GraphQLString
} = require('graphql')

const app = express()

const schema = new GraphQLSchema({
        query: new GraphQLObjectType({
                name: 'Hello World',
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

- It will have a GraphqlObjectType 
- It will have the name
- It will have fields as a function whichi will print the "Hello World"
- Running the server will give an interface and give an error

```
{
  "errors": [
    {
      "message": "Names must match /^[_a-zA-Z][_a-zA-Z0-9]*$/ but \"Hello World\" does not."
    }
  ]
}
```

- This tells us that the name cannot have name
- Remove the space from the name

```js
const express = require('express')
const { graphqlHTTP } = require('express-graphql');

const {
        GraphQLSchema,
        GraphQLObjectType,
        GraphQLString
} = require('graphql')

const app = express()

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

- Query the server
- Checking the Docs will tell us that there is only one query
- That is the `HelloWorld`

```
query {
	message
}
```

- Output

```
{
  "data": {
    "message": "Hello World"
  }
}
```

- The query keyword is not mandatory
- GraphQL by default uses the query keyword

- We can build any type of object by passing it the fields
- Telling it what type those different fields are 
- Resolving what these fields will do

