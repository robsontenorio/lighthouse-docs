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

In this tutorial we will build a simple Blog from scratch using:

- Laravel 5.7
- MySql 
- Lighthouse 

[TODO schema image]

## Basic setup
Create a fresh new laravel project. This sample uses [Laravel Instaler](https://laravel.com/docs/5.7/installation#installing-laravel).  

```bash
laravel new lighthouse-tutorial
```

Install neeeded packages. In this tutorial we will use [Laravel Graphql Playground](https://github.com/mll-lab/laravel-graphql-playground) as IDE. It's like a a powerfull Postman for GraphQL. Of course, we will use Lighthouse as GraphQL Server.

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

> Note that `routes/schema.graphql` was published with sample of a schema. Don't worry about it. Will change it in a while. But before, make sure everything is working fine following next steps.


You can change Lighthouse and Laravel Playground config files, as needed. In this case, will change default namespaces for Models in  `config/lighthouse.php` , in order to keep it same as Laravel default namespaces:

```php
'namespaces' => [
        'models' => 'App',
        ...
];
```

Create a empty `blogdb` database and setup conection variables on  `.env` file 
```bash
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=blogdb
DB_USERNAME=username
DB_PASSWORD=password
```


Run migrations, seed database with some fake users and run up server.
```php
# create tables (DDL)
php artisan migrate

# open tinker shell
php artisan tinker

# run this command inside tinker and exit
factory('App\User', 10)->create();

# run server
php artisan serve

```
Now, your project is up and runing on http://127.0.0.1:8000 .

To make sure everything is working fine, access Laravel GraphQL Playground on http://127.0.0.1:8000/graphql-playround and try some Queries:

```graphql
# find user by id
query{
  user(id: 1)
  {
    id
    name
    email
  }
}
```



## TODO // keep going 