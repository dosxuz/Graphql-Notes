# Introspection Examples

## Fetching the schema using introspection

**query**

```
query Introspection {
  __schema {
    types {
      name
    }
  }
}
```

**output**

```
{
  "data": {
    "__schema": {
      "types": [
        {
          "name": "Query"
        },
        {
          "name": "Book"
        },
        {
          "name": "Int"
        },
        {
          "name": "String"
        },
        {
          "name": "Author"
        },
        {
          "name": "Mutation"
        },
        {
          "name": "Boolean"
        },
        {
          "name": "__Schema"
        },
        {
          "name": "__Type"
        },
        {
          "name": "__TypeKind"
        },
        {
          "name": "__Field"
        },
        {
          "name": "__InputValue"
        },
        {
          "name": "__EnumValue"
        },
        {
          "name": "__Directive"
        },
        {
          "name": "__DirectiveLocation"
        }
      ]
    }
  }
}
```

- This will fetch the schema
- From th schema it will fetch the types
- For each type, it will fetch the names of those types
- Query along with the field names

**query**

```
query Introspection {
  __schema {
    types{
      name
      fields {
        name
        description
        deprecationReason
      }
    }
  }
}
```

**output**

```{
  "data": {
    "__schema": {
      "types": [
        {
          "name": "Query",
          "fields": [
            {
              "name": "book",
              "description": "A single book",
              "deprecationReason": null
            },
            {
              "name": "books",
              "description": "List of Books",
              "deprecationReason": null
            },
            {
              "name": "authors",
              "description": "List of all Authors",
              "deprecationReason": null
            },
            {
              "name": "author",
              "description": "A single author",
              "deprecationReason": null
            }
          ]
        },
        {
          "name": "Book",
          "fields": [
            {
              "name": "id",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "name",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "authorId",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "author",
              "description": null,
              "deprecationReason": null
            }
          ]
        },
        {
          "name": "Int",
          "fields": null
        },
        {
          "name": "String",
          "fields": null
        },
        {
          "name": "Author",
          "fields": [
            {
              "name": "id",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "name",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "books",
              "description": null,
              "deprecationReason": null
            }
          ]
        },
        {
          "name": "Mutation",
          "fields": [
            {
              "name": "addBook",
              "description": "Add a book",
              "deprecationReason": null
            },
            {
              "name": "addAuthor",
              "description": "Add an author",
              "deprecationReason": null
            }
          ]
        },
        {
          "name": "Boolean",
          "fields": null
        },
        {
          "name": "__Schema",
          "fields": [
            {
              "name": "description",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "types",
              "description": "A list of all types supported by this server.",
              "deprecationReason": null
            },
            {
              "name": "queryType",
              "description": "The type that query operations will be rooted at.",
              "deprecationReason": null
            },
            {
              "name": "mutationType",
              "description": "If this server supports mutation, the type that mutation operations will be rooted at.",
              "deprecationReason": null
            },
            {
              "name": "subscriptionType",
              "description": "If this server support subscription, the type that subscription operations will be rooted at.",
              "deprecationReason": null
            },
            {
              "name": "directives",
              "description": "A list of all directives supported by this server.",
              "deprecationReason": null
            }
          ]
        },
        {
          "name": "__Type",
          "fields": [
            {
              "name": "kind",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "name",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "description",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "specifiedByUrl",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "fields",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "interfaces",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "possibleTypes",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "enumValues",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "inputFields",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "ofType",
              "description": null,
              "deprecationReason": null
            }
          ]
        },
        {
          "name": "__TypeKind",
          "fields": null
        },
        {
          "name": "__Field",
          "fields": [
            {
              "name": "name",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "description",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "args",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "type",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "isDeprecated",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "deprecationReason",
              "description": null,
              "deprecationReason": null
            }
          ]
        },
        {
          "name": "__InputValue",
          "fields": [
            {
              "name": "name",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "description",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "type",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "defaultValue",
              "description": "A GraphQL-formatted string representing the default value for this input value.",
              "deprecationReason": null
            },
            {
              "name": "isDeprecated",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "deprecationReason",
              "description": null,
              "deprecationReason": null
            }
          ]
        },
        {
          "name": "__EnumValue",
          "fields": [
            {
              "name": "name",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "description",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "isDeprecated",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "deprecationReason",
              "description": null,
              "deprecationReason": null
            }
          ]
        },
        {
          "name": "__Directive",
          "fields": [
            {
              "name": "name",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "description",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "isRepeatable",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "locations",
              "description": null,
              "deprecationReason": null
            },
            {
              "name": "args",
              "description": null,
              "deprecationReason": null
            }
          ]
        },
        {
          "name": "__DirectiveLocation",
          "fields": null
        }
      ]
    }
  }
}
```

## Query an Object Type 

- You can query an object type and see what fields it has

**query**

```
query Introspection {
  __type(name: "Book") {
    fields {
      name
    }
  }
}
```

**output**

```
{
  "data": {
    "__type": {
      "fields": [
        {
          "name": "id"
        },
        {
          "name": "name"
        },
        {
          "name": "authorId"
        },
        {
          "name": "author"
        }
      ]
    }
  }
}
```

### Creating queries from the gathered information

- From the above information one can create queries to get books name, author and authodId

**query**

```
query DumpData{
  books {
    name
    author {
      name
    }
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
        "name": "Harry Potter and the Philosopher’s Stone",
        "author": {
          "name": "JK Rowling"
        },
        "id": 1
      },
      {
        "name": "Harry Potter and the Chamber of Secrets",
        "author": {
          "name": "JK Rowling"
        },
        "id": 2
      },
      {
        "name": "Harry Potter and the Prisoner of Azkaban",
        "author": {
          "name": "JK Rowling"
        },
        "id": 3
      },
      {
        "name": "A Middle English Vocabular",
        "author": {
          "name": "J.R.R Tokein"
        },
        "id": 4
      },
      {
        "name": "Sir Gawain & The Green Knight",
        "author": {
          "name": "J.R.R Tokein"
        },
        "id": 5
      },
      {
        "name": "The Hobbit: or There and Back Again",
        "author": {
          "name": "J.R.R Tokein"
        },
        "id": 6
      },
      {
        "name": "The Burning White",
        "author": {
          "name": "Brent Weeks"
        },
        "id": 7
      },
      {
        "name": "Way of Shadows",
        "author": {
          "name": "Brent Weeks"
        },
        "id": 8
      }
    ]
  }
}
```

