## Instalation

You must have Node.js version 4.x.x installed, as well as MongoDB version 3.0.
This assumes that you are running MongoDB on the default port 27017.

After that do:

```
$ cd /to/project/directory
$ npm install
```

## Usage

To start the server all you need to to is:
```
$ node index.js
```

If you want to specify a port you can do so by doing:
```
$ node index.js -p 8080
```

The default port is `8080`.


## Model Schemas

There is a User Schema, which holds user information:

```
{
	_id 	: Number,
	email	: String,
	password: String,
	objects : [Number]
}
```

* The `id` field is auto-generated upon user registration. 
* The `objects` array holds user created object ID's.

There is also a Object Schema, which holds object data:

```
{
	_id 	: Number,
	data 	: [Mixed],
	objects : [Number]
}
```

* The `_id` field is not auto-generate, it must be supplied upon object creation (this behaviour can be changed upon request).
* The `data` field is an array of strings and integers.
* The `objects` field is an array of object ID's which is related to.

## Authentication

In order to register and login a User, you must send a HTTP `POST` request to `/register` and `/login` respectively, with a JSON body such as:

```
{
	"email": "example@email.com",
	"password": "somepassword" 
}
```

## Creating Objects

In order to create an Object you must send a HTTP `POST` request to `/objects` with a JSON body such as:

```
{ 
	"id": 1,
	"data": [100, "example", "data", 230],
	"objects": [2,3] // OPTIONAL at this point
}
```

## Updating Objects

In order to update an object you must send a HTTP `POST` request to `/object/id` (the `id` is a number) with a JSON body such as:

```
{
	"data": [100, "example", "data", 230], // OPTIONAL
	"objects": [2,3] // OPTIONAL
}
```

You just need to send the keys that you want to update, being either `data` or `objects`.


## Getting Objects

If you want to retrieve all objects created by one user, just send a HTTP `GET` request to `/objects`. 
The response will contain an array of JSON objects, each element being one Object created by the respective User.

If you want to retrieve one specific object, send a HTTP `GET` request to `/object/id` (the `id` is a number).
The response will contain a JSON object with the Object data. 


## Bugs and questions
Please let me know if you find any bug, or if you want to add/change any feature behaviour.
Questions are also welcome.# gwinfo 
