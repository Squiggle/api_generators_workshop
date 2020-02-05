# Generate a REST interface

## Prerequisites

## Generate OpenAPI

1. Install generator

[OpenAPI Generator commandline](https://openapi-generator.tech/docs/installation)

2. Generate

using aspnetcore generator
outputting to a directory called aspnetcore-demo

```
openapi-generator generate -i schema.yml -g aspnetcore -o aspnetcore-demo
```

3. Run

```
cd aspnetcore-demo/
dotnet build
dotnet run --project src/Org.OpenAPITools/Org.OpenAPITools.csproj 
```

## Generate Postman Collection

1. Install

```
npm install -g openapi-to-postmanv2
```

2. Generate

```
openapi2postmanv2 --spec schema.yml --output postman.json
```

3. Import

Postman 👉 Import

## GraphQL

Hasura is a GraphQL server that exposes a Postgres database as a GraphQL endpoint. This means __the only prerequisite is a series of SQL scripts__. Better still, you can [boot up an instance using Heroku](https://docs.hasura.io/1.0/graphql/manual/getting-started/heroku-simple.html) within minutes.

A competitor, Postgraphile, also performs this task.