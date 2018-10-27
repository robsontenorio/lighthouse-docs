---
id: tutorial
title: Tutorial
---


## What is GraphQL ?

GraphQL is just a specification. Defined by self as a "Query Language for APIs". It provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools.

<br />

[TODO: laravel-playground demo-gif]

<br />

GraphQL has been released only as a *specification*. This means that GraphQL is in fact not more than a long document that describes in detail the behaviour of a GraphQL server. 

<br />

GraphQL has its own type system that’s used to define the schema of an API. The syntax for writing schemas is called Schema Definition Language ([SDL](https://www.prisma.io/blog/graphql-sdl-schema-definition-language-6755bcb9ce51/)).

<br />

Here is an example how we can use the SDL to define a simple type called `Person` and its relationships between another type `Post`:

```graphql
type Person {
  name: String!
  age: Int!
  posts: [Post]
}

type Post {
  title: String!
  author: Person!
}
```
Note that we just created a one-to-many-relationship between `Person` and `Post` since the `posts` field on `Person` is actually an array of `Post`. In another hand, we also defined the inverse relationship from `Post` to `Person` through `author` field.

<br />



**NOTE.** This short intro is a compilation from many sources and all credits goes to its authors.

<br />

- https://graphql.org
- https://howtographql.com



<br />

## What is Lighthouse?

A GraphQL Server for Laravel. Lighthouse is a PHP package that allows you to serve a GraphQL endpoint from your Laravel application. It greatly reduces the boilerplate required to create a schema, integrates well with any Laravel project, and is highly customizable giving you full control over your data.

<br />

1. Write a schema according GraphQL specification;
1. Decorate it with some built-in Lighthouse directives;
1. You have a GraphQL API in a few minutes;

<br />

[TODO: architecture image]

<br />


## Let's do it!

[TODO: from zero to hero]