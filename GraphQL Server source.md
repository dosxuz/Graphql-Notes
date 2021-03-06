# GraphQL Server Code

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
	{ id: 1, name: 'Harry Potter', authorid: 1 },
	{ id: 2, name: 'Some other shit', authorid: 1 },
	{ id: 3, name: 'Baaler chal', authorid: 1 },
	{ id: 4, name: 'Boi er naam', authorid: 2 },
	{ id: 5, name: 'Chudir bhai', authorid: 2 },
	{ id: 6, name: 'chondro gupto', authorid: 2 },
	{ id: 7, name: 'Pod mere', authorid: 3 },
	{ id: 8, name: 'Gondo shukto', authorid: 3 }
]

const BookType = new GraphQLObjectType({
	name: 'Book',
	description: 'This represents a book written by an author',
	fields: () => ({
		id: { type: GraphQLNonNull(GraphQLInt) },
		name: { type: GraphQLNonNull(GraphQLString) },
		authorId: { type: GraphQLNonNull(GraphQLInt) },
		author: {
			type: AuthorType,
			resolve: (book) => {
				return authors.find(author => author.id == book.authorid)
			}
		}
	})
})


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

const schema = new GraphQLSchema ({
	query: RootQueryType,
	mutation: RootMutationType
})


app.use('/graphql', graphqlHTTP({
	schema: schema,
	graphiql: true
}))

app.listen(5000., () => console.log('Server Running'))
```