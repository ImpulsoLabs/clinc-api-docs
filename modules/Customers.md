# Customers

## Properties

Customers don´t have an `ID`. **All fields except for `email` are OPTIONAL**.

| Property  | Description |
| ------------- | ------------- |
| email  |  The `email` is the unique identifier of the user. It can´t be updated or repeated between users.  |
| name | String. Name of the customer.  |
| phone | String. Phone of the customer. |
| age | Integer. Age of the customer. |
| gender | String. Gender of the customer. |
| city | String. City of the customer. |
| country | String. Country of the customer. |

# Endpoints

## GET /customers

Customers are paginated.  

**Parameters:**

| Param  | Description |
| ------------- | ------------- |
| email | Useful to search a specific customer |
| page  | Page number (Default 1)  |
| page_size  |  Size of the page (Maximum 50, Default 10) |


### GET /customers

Returns a list of customers

`GET /customers`

```
[
  {
    "email": "markjohnson@fakemail.com",
    "name": "Mark Johnson",
    "phone": "16 9547 63214",
    "age": 27,
    "gender": "male",
    "city": "Chicago",
    "country": "United States"
  },
  {
    "email": "taniaperez@fakemail.com",
    "name": null,
    "phone": null,
    "age": null,
    "gender": null,
    "city": null,
    "country": null
  },
  {
    "email": "pauleriksen@fakemail.com",
    "name": "Paul Eriksen",
    "phone": "11 3695 2548",
    "age": 39,
    "gender": "male",
    "city": "Buenos Aires",
    "country": "Argentina"
  }
]
```
  
### GET /customers?email={CUSTOMER_EMAIL}

`GET /customers?email=pauleriksen@fakemail.com`

```
[
  {
    "email": "pauleriksen@fakemail.com"
    "name": "Paul Eriksen",
    "phone": "11 3695 2548",
    "age": 39,
    "gender": "male",
    "city": "Buenos Aires",
    "country": "Argentina"
  }
]
```

## POST /customers

The only mandatory field for creating customers is the `email`. If everything goes ok you will receive the same customer in response.

Creating a new customer:

### POST /customers

**Body:**

```
{
  "email": "paulasuarez@fakemail.com"
  "name": "Paula Suarez",
  "gender": "female",
  "city": "Sidney",
  "country": "Australia"
}
```

**Response:**

```
{
  "email": "paulasuarez@fakemail.com"
  "name": "Paula Suarez",
  "phone": null,
  "age": null,
  "gender": "female",
  "city": "Sidney",
  "country": "Australia"
}
```

## PUT /customers

To update a customer, is necesary to specify the `email` in the body object. As it is clarified above, the `email` can´t be updated.

### PUT /customers

Updating a customer.

`PUT /customers`  

**Body:**

```
{
  "email": "taniaperez@fakemail.com",
  "name": "Tania Perez",
  "age": 25,
  "gender": "female"
}
```

**Response:**

```
{
  "email": "taniaperez@fakemail.com",
  "name": "Tania Perez",
  "phone": null,
  "age": 25,
  "gender": "female",
  "city": null,
  "country": null
}
```

## DELETE /customers

Only customers which don´t have orders associated can be deleted, by passing the `email` as parameter in the URL. The success response is an empty object.

### DELETE /customers?email={CUSTOMER_EMAIL}

`DELETE /customers?email=markjohnson@fakemail.com`  

**Response:**

```
{}
```




