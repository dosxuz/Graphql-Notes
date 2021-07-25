# What is Graphql

- Specific application bulit on http about how you get around the server.
- The way you determine what data you get back from the endpoint is based on the query which you use

## Difference between Restful API and Graphql

### With Restful API 

- We need a particular endpoint we need to ge the particular data
- We might get unnecessary information : `/authors` endpoint to get the information about the authors
- We need another endpoint for accessing more data : `/authors/:id/books`

### WIth GraphQL

- We can get specific information

```graphql
query {
authors {
name
books {
name
}
}
}
```

- We get the author name, books written by the author and books name
- We give the simple query to the server and the server parses that query 
- We get only the information that we ask for
