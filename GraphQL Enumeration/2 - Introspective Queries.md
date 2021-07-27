# Introspective Queries

- `__` are exclusively for introspective queries

## Different Introspective Queries

- `__schema` is the primary source and enables us to fetch the whole schema
- `types` tells us what types the schema has
- `__type(name:"User")` specifically get the type using an argument
- `queryType` tells us the available query operations in the schema