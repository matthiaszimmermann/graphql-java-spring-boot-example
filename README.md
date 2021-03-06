# graphql-java-spring-boot-example
Sample app for my tutorial [Building a GraphQL Server with Spring Boot](https://www.pluralsight.com/guides/building-a-graphql-server-with-spring-boot). 

For testing [Java 11](https://adoptopenjdk.net/installation.html?variant=openjdk11&jvmVariant=hotspot#) can be usede with this repo (The original repo seemst to have been tested with [Java 9](http://www.oracle.com/technetwork/java/javase/downloads/jdk9-downloads-3848520.html)).

Clone this repo and execute `mvnw spring-boot:run`. Or inside an IDE, execute the class `com.example.DemoGraphQL.DemoGraphQlApplication`.

You can go to [http://localhost:8080/h2-console/login.jsp](http://localhost:8080/h2-console/login.jsp) and enter the following information:
- JDBC URL: jdbc:h2:mem:testdb
- User Name: sa
- Password: <blank>

## Run Examples

You may use curl on the command line

```
curl -X POST -H "Content-Type: application/json" -d '{"query": "{findAllBooks{id title}}"}' http://localhost:8080/graphql
```

Or the built-in graphical user interface [http://localhost:8080/graphiql](http://localhost:8080/graphiql) to start executing queries.

```
{
  findAllBooks {
    id
    isbn
    title
    pageCount
    author {
      firstName
      lastName
    }
  }
}
```

Or:
```
mutation {
  newBook(
    title: "Java: The Complete Reference, Tenth Edition", 
    isbn: "1259589331", 
    author: 1) {
      id title
  }
}
```
## Run Error Case Examples

Ask for non-existing attribute
```
{
  findAllBooks {
    id
    title
    publisher
  }
}
```

Try to update a non-existing book
```
mutation {
  updateBookPageCount(pageCount: 1313 id: 3)
     {
      id
      title
      pageCount
    }
}
```
# A Java Client would be nice ...

SpringBoot provides support to intuitively build GraphQL server apps. Unfortunately, java client support is lacking. The list below provides some pointers to using Java for building GraphQL clients.

GraphQL Java Client Links
* [DZone Article with some comments regarding clients](https://dzone.com/articles/graphql-the-future-of-microservices)
* [Node Library from Americanexpress](https://americanexpress.io/graphql-for-the-jvm/)
* [Shopify Library](https://github.com/Shopify/graphql_java_gen)
* [Android Apollo Library](https://github.com/apollographql/apollo-android)

TODO
* check out [MountCloud client lib](https://github.com/MountCloud/graphql-client)
* check out [hasura GraphQL on Postgres](https://github.com/hasura/graphql-engine)

# License
MIT
