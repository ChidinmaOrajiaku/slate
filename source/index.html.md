---
title: HelloBooks API

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Hello-Books is a simple application that helps manage a library and its processes like stocking, tracking and renting books. With this application users are able to find and rent books. The application also has an admin section where the admin can add books, delete books, edit books, increase the quantity of a book etc.

# Development

The application was developed with [Node.js-Express](https://docs.npmjs.com/getting-started/installing-node). The [PostgreSQL](https://www.postgresql.org/download/) database was used with Sequelize as the ORM

# Installation

1. Ensure you have NodeJs and PostgreSQL installed
2. Clone the repository https://github.com/ChidinmaOrajiaku/HelloBooksProject.git
3. Change your directory "cd HelloBooksProject"
4. Install all dependencies "npm install"
5. Start the app with "npm start:serv" for development 
6. Use [Postman](https://www.getpostman.com/) to consume the API

# Authentication

All routes are jwt-token protected. On login (with email and password), a token is generated. HelloBooks expects the token to be included in the body or headers as x-token. All API requests to the server are stated below.

# Api Summary

Below are the endpoints and thier functionalities
<table>
<tr>
<th> API</th>
<th> Functionality </th>
</tr>

<tr>
<td>POST /api/v1/users/signup </td>
<td> Create new users </td>
</tr>

<tr>
<td>POST /api/v1/users/signin </td>
<td> Login users </td>
</tr>

<tr>
<td>GET /api/v1/users/:userId</td>
<td> Get user details </td>
</tr>

<tr>
<td>PUT /api/v1/users/:userId </td>
<td> Update password </td>
</tr>

<tr>
<td>GET /api/v1/users/books </td>
<td> List all books </td>
</tr>

<tr>
<td>GET /api/v1/books/:id </td>
<td> List a book </td>
</tr>

<tr>
<td>POST /api/v1/users/:userId/books </td>
<td> Borrow a book </td>
</tr>

<tr>
<td>GET /api/v1/users/:userId/history </td>
<td> List all books borrowed </td>
</tr>

<tr>
<td>GET /api/v1/users/:userId/books </td>
<td> List all books borrowed but not returned </td>
</tr>

<tr>
<td>PUT /api/v1/users/:userId/books </td>
<td> Return book borrowed </td>
</tr>

<tr>
<td>GET /api/v1/users </td>
<td> Admin count all users </td>
</tr>

<tr>
<td>POST /api/v1/users/books </td>
<td> Admin add books </td>
</tr>

<tr>
<td>PUT /api/v1/books/:bookId </td>
<td> Admin modify books </td>
</tr>

<tr>
<td>DELETE /api/v1/books/:bookId </td>
<td> Admin delete books </td>
</tr>

<tr>
<td>GET /api/v1/books </td>
<td> Admin count all books </td>
</tr>

<tr>
<td>GET /api/v1/users/books/history </td>
<td> Admin count all rented books </td>
</tr>

<tr>
<td>GET /api/v1/users/books/unreturned/history </td>
<td> Admin count all not returned books </td>
</tr>

<tr>
<td>GET /api/v1/users/books/unreturned </td>
<td> Admin list all not returned books </td>
</tr>

<tr>
<td>POST /api/v1/books/category </td>
<td> Admin create category </td>
</tr>

<tr>
<td>GET /api/v1/books/category/history </td>
<td> Admin count category </td>
</tr>

<tr>
<td>GET /api/v1/books/category/all </td>
<td> Admin list all categories </td>
</tr>
<table/>

# Users

## Sign Up

> Request

```json
{
	"firstname": "daddy",
	"lastname": "daddy",
	"username": "daddy",
	"password": "daddy",
	"email": "daddy@gmail.com"
}
```
> Response

```json
{
    "message": "Account created! Proceed to login",
    "username": "daddy"
}
```

This endpoint creates a new user.

### HTTP Request

`POST https://hello-books-bootcamp.herokuapp.com/api/v1/users/signup`

### Request

* Body (application/json)

### Response

* Status: 201 created
* Body (application/json)

## Login

> Request

```json
{
	"password": "daddy",
	"email": "daddy@gmail.com"
}
```
> Response

```json
{
    "message": "Successfully logged in",
    "username": "daddy",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImRhZGR5Iiwicm9sZSI6InVzZXIiLCJpZCI6MTAsImlhdCI6MTUxMjk5NDM2OCwiZXhwIjoxNTEzMDgwNzY4fQ.hjUauS-WAvRUEM4xZYgTkJzdhUmNYpSttK35FO8CvW4"
}
```

This endpoint logs in user.

### HTTP Request

`POST https://hello-books-bootcamp.herokuapp.com/api/v1/users/signin`

### Request

* Body (application/json)

### Response

* Status: 200 success
* Body (application/json)


## Get user details

> Response

```json
{
    "firstname": "daddy",
    "lastname": "daddy",
    "email": "daddy@gmail.com",
    "username": "daddy"
}
```

This endpoint gets the user details.

### HTTP Request

`GET https://hello-books-bootcamp.herokuapp.com/api/v1/users/:userId`

### Request

* Body (application/json)
* userId: 10

### Response

* Status: 200 success
* Body (application/json)


## Update user password

> Request

```json
{
	"password": "daddy2",
	"verifyPassword": "daddy"
}
```

> Response

```json
{
    "message": "Succesfully Updated"
}
```

This endpoint updates the user password.

### HTTP Request

`PUT https://hello-books-bootcamp.herokuapp.com/api/v1/users/:userId`

### Request

* Body (application/json)
* userId: 10

### Response

* Status: 200 success
* Body (application/json)

## List all books

> Response

```json
[
    {
        "id": 1,
        "title": "Blue Smoke",
        "author": "Nora Roberts",
        "category": "Fiction",
        "image": "https://res.cloudinary.com/andela-chidinma/image/upload/v1511133007/g2exfx6sgbymszspybts.jpg",
        "review": "Nice Book",
        "createdAt": "2017-11-19T23:10:10.090Z",
        "updatedAt": "2017-11-19T23:10:10.090Z",
        "userId": null,
        "categoryId": null
    },
    {
        "id": 2,
        "title": "Blue Smoke",
        "author": "Nora Roberts",
        "category": "Fiction",
        "image": "https://res.cloudinary.com/andela-chidinma/image/upload/v1511133007/g2exfx6sgbymszspybts.jpg",
        "review": "Nice Book",
        "createdAt": "2017-11-19T23:11:27.100Z",
        "updatedAt": "2017-11-22T11:36:41.413Z",
        "userId": null,
        "categoryId": null
    }
]
```

This endpoint allows the user get all books.

### HTTP Request

`GET https://hello-books-bootcamp.herokuapp.com/api/v1/users/books`

### Request

* Body (application/json)

### Response

* Status: 200 success
* Body (application/json)

## List a book

> Response

```json
{
    "id": 1,
    "title": "Blue Smoke",
    "author": "Nora Roberts",
    "category": "Fiction",
    "image": "https://res.cloudinary.com/andela-chidinma/image/upload/v1511133007/g2exfx6sgbymszspybts.jpg",
    "review": "Nice Book",
    "createdAt": "2017-11-19T23:10:10.090Z",
    "updatedAt": "2017-11-19T23:10:10.090Z",
    "userId": null,
    "categoryId": null
}
```

This endpoint gets a book.

### HTTP Request

`GET https://hello-books-bootcamp.herokuapp.com/api/v1/books/:id`

### Request

* Body (application/json)
* id: 1

### Response

* Status: 200 success
* Body (application/json)

## Borrow a book

> Request

```json
{
	"bookId": "1"
}
```

> Response

```json
{
    "returned": false,
    "id": 11,
    "userId": 10,
    "bookId": 1,
    "toReturnDate": "2018-01-04",
    "updatedAt": "2017-12-11T12:41:50.644Z",
    "createdAt": "2017-12-11T12:41:50.644Z",
    "returnDate": null,
    "categoryId": null
}
```

This endpoint allows the user borrow a book.

### HTTP Request

`POST https://hello-books-bootcamp.herokuapp.com/api/v1/users/:userId/books`

### Request

* Body (application/json)
* userId: 10

### Response

* Status: 200 success
* Body (application/json)

## List all books borrowed

> Response

```json
[
    {
        "id": 11,
        "bookId": 1,
        "returned": false,
        "toReturnDate": "2018-01-04",
        "returnDate": null,
        "userId": 10,
        "createdAt": "2017-12-11T12:41:50.644Z",
        "updatedAt": "2017-12-11T12:41:50.644Z",
        "categoryId": null,
        "Book": {
            "id": 1,
            "title": "Blue Smoke",
            "author": "Nora Roberts",
            "category": "Fiction",
            "image": "https://res.cloudinary.com/andela-chidinma/image/upload/v1511133007/g2exfx6sgbymszspybts.jpg",
            "review": "Nice Book",
            "createdAt": "2017-11-19T23:10:10.090Z",
            "updatedAt": "2017-11-19T23:10:10.090Z",
            "userId": null,
            "categoryId": null
        },
        "Category": null
    }
]
```

This endpoint allows the user get all books borrowed.

### HTTP Request

`GET https://hello-books-bootcamp.herokuapp.com/api/v1/users/:userId/history`

### Request

* Body (application/json)
* userId: 10

### Response

* Status: 200 success
* Body (application/json)

## List all books borrowed but not returned

> Response

```json
[
    {
        "id": 11,
        "bookId": 1,
        "returned": false,
        "toReturnDate": "2018-01-04",
        "returnDate": null,
        "userId": 10,
        "createdAt": "2017-12-11T12:41:50.644Z",
        "updatedAt": "2017-12-11T12:41:50.644Z",
        "categoryId": null,
        "Book": {
            "id": 1,
            "title": "Blue Smoke",
            "author": "Nora Roberts",
            "category": "Fiction",
            "image": "https://res.cloudinary.com/andela-chidinma/image/upload/v1511133007/g2exfx6sgbymszspybts.jpg",
            "review": "Nice Book",
            "createdAt": "2017-11-19T23:10:10.090Z",
            "updatedAt": "2017-11-19T23:10:10.090Z",
            "userId": null,
            "categoryId": null
        },
        "Category": null
    }
]
```

This endpoint allows the user get all books borrowed.

### HTTP Request

`GET https://hello-books-bootcamp.herokuapp.com/api/v1/users/:userId/books`

### Request

* Body (application/json)
* userId: 10

### Response

* Status: 200 success
* Body (application/json)

## Return book borrowed

> Request

```json
{
	"bookId": "1"
}
```

> Response

```json
{
    "message": "Successfully Returned"
}
```

This endpoint allows the user return book borrowed.

### HTTP Request

`PUT https://hello-books-bootcamp.herokuapp.com/api/v1/users/:userId/books`

### Request

* Body (application/json)
* userId: 10

### Response

* Status: 200 success
* Body (application/json)


# Admin

<aside class="notice">This section can only be accessed by the administrator using an admin token. </aside>

## Admin count all users

> Response

```json
{
    "count": 5
}
```

This endpoint counts all users.

### HTTP Request

`GET https://hello-books-bootcamp.herokuapp.com/api/v1/users`

### Request

* Body (application/json)

### Response

* Status: 200 success
* Body (application/json)

## Admin add books

> Request

```json
{
	"title": "Morning, Noon and Night",
	"author": "Sidney Sheldon",
	"category": "Fiction",
	"image": "https://images.gr-assets.com/books/1348785812l/900012.jpg",
	"review": "Nice Book"
}
```

> Response

```json
{
    "message": "Succesfully added"
}
```

This endpoint adds a new book.

### HTTP Request

`POST https://hello-books-bootcamp.herokuapp.com/api/v1/users/books`

### Request

* Body (application/json)

### Response

* Status: 201 created
* Body (application/json)

## Admin modify books

> Request

```json
{
	"title": "Morning, Noon and Night",
	"author": "Sidney",
	"category": "Fiction",
	"image": "https://images.gr-assets.com/books/1348785812l/900012.jpg",
	"review": "Nice Book"
}
```

> Response

```json
{
    "id": 4,
    "title": "Morning, Noon and Night",
    "author": "Sidney",
    "category": "Fiction",
    "image": "https://images.gr-assets.com/books/1348785812l/900012.jpg",
    "review": "Nice Book",
    "createdAt": "2017-12-11T13:37:54.425Z",
    "updatedAt": "2017-12-11T13:46:22.744Z",
    "userId": null,
    "categoryId": null
}
```

This endpoint modifies a book.

### HTTP Request

`PUT https://hello-books-bootcamp.herokuapp.com/api/v1/books/:bookId`

### Request

* Body (application/json)
* bookId: 4

### Response

* Status: 200 success
* Body (application/json)

## Admin delete books

This endpoint deletes a book.

### HTTP Request

`DELETE https://hello-books-bootcamp.herokuapp.com/api/v1/books/:bookId`

### Request

* Body (application/json)
* bookId: 4

### Response

* Status: 204 No content
* Body (application/json)

## Admin count all books

> Response

```json
{
    "count": 2,
    "rows": [
        {
            "id": 1,
            "title": "Blue Smoke",
            "author": "Nora Roberts",
            "category": "Fiction",
            "image": "https://res.cloudinary.com/andela-chidinma/image/upload/v1511133007/g2exfx6sgbymszspybts.jpg",
            "review": "Nice Book",
            "createdAt": "2017-11-19T23:10:10.090Z",
            "updatedAt": "2017-11-19T23:10:10.090Z",
            "userId": null,
            "categoryId": null
        },
        {
            "id": 2,
            "title": "Blue Smoke",
            "author": "Nora Roberts",
            "category": "Fiction",
            "image": "https://res.cloudinary.com/andela-chidinma/image/upload/v1511133007/g2exfx6sgbymszspybts.jpg",
            "review": "Nice Book",
            "createdAt": "2017-11-19T23:11:27.100Z",
            "updatedAt": "2017-11-22T11:36:41.413Z",
            "userId": null,
            "categoryId": null
        }
    ]
}
```

This endpoint counts books in the library.

### HTTP Request

`GET https://hello-books-bootcamp.herokuapp.com/api/v1/books`

### Request

* Body (application/json)

### Response

* Status: 200 success
* Body (application/json)

## Admin count all rented books

> Response

```json
{
    "count": 2,
    "rows": [
        {
            "id": 1,
            "title": "Blue Smoke",
            "author": "Nora Roberts",
            "category": "Fiction",
            "image": "https://res.cloudinary.com/andela-chidinma/image/upload/v1511133007/g2exfx6sgbymszspybts.jpg",
            "review": "Nice Book",
            "createdAt": "2017-11-19T23:10:10.090Z",
            "updatedAt": "2017-11-19T23:10:10.090Z",
            "userId": null,
            "categoryId": null
        },
        {
            "id": 2,
            "title": "Blue Smoke",
            "author": "Nora Roberts",
            "category": "Fiction",
            "image": "https://res.cloudinary.com/andela-chidinma/image/upload/v1511133007/g2exfx6sgbymszspybts.jpg",
            "review": "Nice Book",
            "createdAt": "2017-11-19T23:11:27.100Z",
            "updatedAt": "2017-11-22T11:36:41.413Z",
            "userId": null,
            "categoryId": null
        }
    ]
}
```

This endpoint counts rentedbooks in the library.

### HTTP Request

`GET https://hello-books-bootcamp.herokuapp.com/api/v1/users/books/history`

### Request

* Body (application/json)

### Response

* Status: 200 success
* Body (application/json)

## Admin count all not returned books

> Response

```json
{
    "count": 6,
}
```

This endpoint counts all not returned books.

### HTTP Request

`GET https://hello-books-bootcamp.herokuapp.com/api/v1/users/books/unreturned/history`

### Request

* Body (application/json)

### Response

* Status: 200 success
* Body (application/json)

## Admin list all not returned books

> Response

```json
[
    {
        "id": 1,
        "bookId": null,
        "returned": false,
        "toReturnDate": "2017-12-16",
        "returnDate": null,
        "userId": 1,
        "createdAt": "2017-11-22T16:52:28.005Z",
        "updatedAt": "2017-11-22T16:52:28.005Z",
        "categoryId": null,
        "Book": null,
        "Category": null
    },
    {
        "id": 3,
        "bookId": 1,
        "returned": false,
        "toReturnDate": "2017-12-20",
        "returnDate": null,
        "userId": 1,
        "createdAt": "2017-11-26T14:06:40.212Z",
        "updatedAt": "2017-11-26T14:06:40.212Z",
        "categoryId": null,
        "Book": {
            "id": 1,
            "title": "Blue Smoke",
            "author": "Nora Roberts",
            "category": "Fiction",
            "image": "https://res.cloudinary.com/andela-chidinma/image/upload/v1511133007/g2exfx6sgbymszspybts.jpg",
            "review": "Nice Book",
            "createdAt": "2017-11-19T23:10:10.090Z",
            "updatedAt": "2017-11-19T23:10:10.090Z",
            "userId": null,
            "categoryId": null
        },
        "Category": null
    },
    {
        "id": 4,
        "bookId": 2,
        "returned": false,
        "toReturnDate": "2017-12-20",
        "returnDate": null,
        "userId": 2,
        "createdAt": "2017-11-26T15:08:11.151Z",
        "updatedAt": "2017-11-26T15:08:11.151Z",
        "categoryId": null,
        "Book": {
            "id": 2,
            "title": "Blue Smoke",
            "author": "Nora Roberts",
            "category": "Fiction",
            "image": "https://res.cloudinary.com/andela-chidinma/image/upload/v1511133007/g2exfx6sgbymszspybts.jpg",
            "review": "Nice Book",
            "createdAt": "2017-11-19T23:11:27.100Z",
            "updatedAt": "2017-11-22T11:36:41.413Z",
            "userId": null,
            "categoryId": null
        },
        "Category": null
    },
    {
        "id": 5,
        "bookId": 1,
        "returned": false,
        "toReturnDate": "2017-12-20",
        "returnDate": null,
        "userId": 2,
        "createdAt": "2017-11-26T15:08:39.138Z",
        "updatedAt": "2017-11-26T15:08:39.138Z",
        "categoryId": null,
        "Book": {
            "id": 1,
            "title": "Blue Smoke",
            "author": "Nora Roberts",
            "category": "Fiction",
            "image": "https://res.cloudinary.com/andela-chidinma/image/upload/v1511133007/g2exfx6sgbymszspybts.jpg",
            "review": "Nice Book",
            "createdAt": "2017-11-19T23:10:10.090Z",
            "updatedAt": "2017-11-19T23:10:10.090Z",
            "userId": null,
            "categoryId": null
        },
        "Category": null
    },
    {
        "id": 10,
        "bookId": 1,
        "returned": false,
        "toReturnDate": "2017-12-20",
        "returnDate": null,
        "userId": 8,
        "createdAt": "2017-11-26T19:07:48.599Z",
        "updatedAt": "2017-11-26T19:07:48.599Z",
        "categoryId": null,
        "Book": {
            "id": 1,
            "title": "Blue Smoke",
            "author": "Nora Roberts",
            "category": "Fiction",
            "image": "https://res.cloudinary.com/andela-chidinma/image/upload/v1511133007/g2exfx6sgbymszspybts.jpg",
            "review": "Nice Book",
            "createdAt": "2017-11-19T23:10:10.090Z",
            "updatedAt": "2017-11-19T23:10:10.090Z",
            "userId": null,
            "categoryId": null
        },
        "Category": null
    },
    {
        "id": 11,
        "bookId": 1,
        "returned": false,
        "toReturnDate": "2018-01-04",
        "returnDate": null,
        "userId": 10,
        "createdAt": "2017-12-11T12:41:50.644Z",
        "updatedAt": "2017-12-11T12:41:50.644Z",
        "categoryId": null,
        "Book": {
            "id": 1,
            "title": "Blue Smoke",
            "author": "Nora Roberts",
            "category": "Fiction",
            "image": "https://res.cloudinary.com/andela-chidinma/image/upload/v1511133007/g2exfx6sgbymszspybts.jpg",
            "review": "Nice Book",
            "createdAt": "2017-11-19T23:10:10.090Z",
            "updatedAt": "2017-11-19T23:10:10.090Z",
            "userId": null,
            "categoryId": null
        },
        "Category": null
    }
]
```

This endpoint list all not returned books.

### HTTP Request

`GET https://hello-books-bootcamp.herokuapp.com/api/v1/users/books/unreturned`

### Request

* Body (application/json)

### Response

* Status: 200 success
* Body (application/json)

## Admin add category

> Request

```json
{
	"category": "Comic"
}
```

> Response

```json
{
    "id": 2,
    "category": "Comic",
    "updatedAt": "2017-12-11T14:11:59.065Z",
    "createdAt": "2017-12-11T14:11:59.065Z",
    "userId": null
}
```

This endpoint adds category.

### HTTP Request

`POST https://hello-books-bootcamp.herokuapp.com/api/v1/books/category`

### Request

* Body (application/json)

### Response

* Status: 201 created
* Body (application/json)

## Admin count category

> Response

```json
{
    "count": 2,
}
```

This endpoint counts category.

### HTTP Request

`GET https://hello-books-bootcamp.herokuapp.com/api/v1/books/category`

### Request

* Body (application/json)

### Response

* Status: 200 success
* Body (application/json)

## Admin list all categories

> Response

```json
[
    {
        "id": 1,
        "category": "Fiction",
        "createdAt": "2017-11-19T23:07:12.681Z",
        "updatedAt": "2017-11-19T23:07:12.681Z",
        "userId": null
    },
    {
        "id": 2,
        "category": "Comic",
        "createdAt": "2017-12-11T14:11:59.065Z",
        "updatedAt": "2017-12-11T14:11:59.065Z",
        "userId": null
    }
]
```

This endpoint lists all categories

### HTTP Request

`GET https://hello-books-bootcamp.herokuapp.com/api/v1/books/category/all`

### Request

* Body (application/json)

### Response

* Status: 200 success
* Body (application/json)