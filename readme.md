Demonstrations of quick-start API tooling:
- Using OpenAPI Generators to create a REST service from an OpenAPI schema
- Using Postman to create a mock endpoint from an OpenAPI schema
- Using Hasura to create a GraphQL API from a database schema

Before begining, familiarise yourself with the OpenAPI Schema `schema.yml`.

# Generating a REST server

## 1. Install the OpenAPI command line tools

[OpenAPI Generator commandline](https://openapi-generator.tech/docs/installation)

## 2. Generate

For this demonstration we'll use using the `aspnetcore` generator, which will create a new server project.

```
cd openapi
openapi-generator generate -i schema.yml -g aspnetcore -o aspnetcore-demo
```

## 3. Run the code

_Ensure you have the relevant version of dotnet core installed_:

```
cd aspnetcore-demo/src/Org.OpenAPITools/
dotnet run
```

Which will launch the new server on localhost.

# Generate Postman Collection

1. Open Postman
2. Import > `schema.yml` selecting "Generate Postman Collection"
3. Open the options for `example-api` and select "Mock Collection"

This will provide you with a URL which performs the same functionality as the service we generated above, but hosted by Postman. _Note that requests are throttled in the free version_.

# GraphQL

Hasura is a GraphQL server that exposes a Postgres database as a GraphQL endpoint. This means __the only prerequisite is a series of SQL scripts__. Better still, you can [boot up an instance using Heroku](https://docs.hasura.io/1.0/graphql/manual/getting-started/heroku-simple.html) within minutes. A competitor, Postgraphile, also performs this task.

This demonstration requires docker.

## 1. Launch Hasura and Postgres

```
cd graphql
docker-compose up -d
```

## 2. Populate the database

Navigate to the Hasura SQL console at http://localhost:8080/console/data/sql

Create the table and populate it using the following SQL scripts:

```
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    name VARCHAR(255) NOT NULL
);

INSERT INTO users (id, name) VALUES (1, 'Alexis');
INSERT INTO users (id, name) VALUES (2, 'Billy');
INSERT INTO users (id, name) VALUES (3, 'Chris');
```

## 3. Run a query

Using `curl` to query the GraphQL endpoint:

```
curl -d '{"query":"{users{id,name}}"}' -H "Content-Type: application/json" -X POST http://localhost:8080/v1/graphql | jq
```

# Resources

- [OpenAPI specification](https://swagger.io/docs/specification/about/)
- [OpenAPI Generators](https://openapi-generator.tech/)
- [Hasura](https://hasura.io)
- [Postgraphile](https://www.graphile.org/postgraphile/)
