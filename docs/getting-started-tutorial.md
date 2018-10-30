---
id: tutorial
title: Tutorial
---


## What is GraphQL ?

GraphQL is just a specification. Defined by self as a "Query Language for APIs". It provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools.

<br />

<div align="center">
  <img src="/docs/assets/tutorial/playground.png">  
  <small>GraphQL Playground</small>
</div>

<br />

GraphQL has been released only as a *specification*. This means that GraphQL is in fact not more than a long document that describes in detail the behaviour of a GraphQL server. 

So, GraphQL has its own type system that’s used to define the schema of an API. The syntax for writing schemas is called Schema Definition Language ([SDL](https://www.prisma.io/blog/graphql-sdl-schema-definition-language-6755bcb9ce51/)).


Here is an example how we can use the SDL to define a simple type called `Person` and its relationships between another type `Post`. This is a pure GraphQL schema definition, regardless of frameworks.

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

> This short intro above is a compilation from many sources and all credits goes to its authors.
> - https://graphql.org
> - https://howtographql.com

<br />

## What is Lighthouse?

A GraphQL Server for Laravel. Lighthouse is a PHP package that allows you to serve a GraphQL endpoint from your Laravel application. It greatly reduces the boilerplate required to create a schema, integrates well with any Laravel project, and is highly customizable giving you full control over your data.

1. Write a schema according GraphQL specification;
1. Decorate it with some built-in Lighthouse directives;
1. You have a GraphQL API in a few minutes;

<br />

[TODO: architecture image]

<br />


## Let's do it!

In this tutorial we will build a simple Blog from scratch. One user can publish many posts, and each post has many comments.

<div align="center">
  <img src="/docs/assets/tutorial/model.png">  
  <p><small>Diagram</small></p>
</div>

Our tools:

- Laravel 5.7
- MySql 
- Lighthouse 
- Laravel GraphQL Playground

<br />

## Basic setup

Create a fresh new laravel project.

```bash
laravel new lighthouse-tutorial
```

In this tutorial we will use [Laravel Graphql Playground](https://github.com/mll-lab/laravel-graphql-playground) as IDE. It's like a Postman for GraphQL, but with super powers. Of course, we will use Lighthouse as GraphQL Server.

```bash
composer require nuwave/lighthouse mll-lab/laravel-graphql-playground
```

Then publish vendor config files
```bash
# lighthouse
php artisan vendor:publish --provider="Nuwave\Lighthouse\Providers\LighthouseServiceProvider"

# playground
php artisan vendor:publish --provider="MLL\GraphQLPlayground\GraphQLPlaygroundServiceProvider"
```

> At this point note that `routes/schema.graphql` was published with sample schema. Don't worry about it. We will change it in a while. But before, make sure everything is working fine with default install  following next steps.

<br />

You can change Lighthouse and Laravel Playground config files, as needed. In this case, change default namespaces for Models in  `config/lighthouse.php` , in order to keep it same as Laravel default namespaces.

```php
'namespaces' => [
        'models' => 'App', 
        ...
],
```

Make sure to create a empty `blog_db` database and set up connection variables in  `.env` file 

```bash
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=blog_db
DB_USERNAME=username
DB_PASSWORD=password
```


Run migrations, seed database with some fake users and start the server.

```php
# create tables (DDL)
php artisan migrate

# open tinker shell
php artisan tinker

# run this command inside tinker and exit
factory('App\User', 10)->create();

# start the server
php artisan serve

```

To make sure everything is working fine, access Laravel GraphQL Playground on http://127.0.0.1:8000/graphql-playground and try some Queries:

```graphql
query {
  user(id: 1) {
    id
    name
    email
  }
}
```

## TODO // keep going 