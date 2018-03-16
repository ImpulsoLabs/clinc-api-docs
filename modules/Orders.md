# Orders

## Properties

| Property  | Description |
| ------------- | ------------- |
| id  | Order `ID` in your eCommerce.  |
| total  |  Double. Total amount of the order. |
| currency | Currency ISO code of the currency used in the order. Check [Currency ISO values](http://www.xe.com/iso4217.php).  
| status | String. Current status of the order. (OPTIONAL) |
| items | Array of objects. Each object must contain the `product_variant_id` and the `quantity`, example: `[{ "product_variant_id":1, "quantity": 20 }, { "product_variant_id":4, "quantity": 6 }]`  |
| customer | Object with the customer data. Check [Customers](Customers.md). |
| shipping | Object with shipping data (OPTIONAL). Shipping fields: `status`, `cost`, `name` and `address`. All fields are optional.  |
| payment | Object with payment data (OPTIONAL). Payment fields: `status`, `status_detail` `type` and `id` (in case you have an `ID` associated with the payment). All fields are optional. |

# Endpoints

## GET /orders

Orders are paginated.  

**Parameters:**

| Param  | Description |
| ------------- | ------------- |
| customer_email  | Useful to search orders for a specific customer.  |
| page  | Page number (Default 1)  |
| page_size  |  Size of the page (Maximum 50, Default 10) |


### GET /orders

Returns a list of orders.

`GET /orders`

```
[
  {
    "id": 23,
    "total": 200.5
    "currency": "USD",
    "status": "closed",
    "items": [
      {
        "product_variant_id: 1,
        "quantity": 20
      },
      {
        "product_variant_id": 4,
        "quantity": 6
      }
    ],
    "customer": {
      "email": "pauleriksen@fakemail.com"
      "name": "Paul Eriksen",
      "phone": "11 3695 2548",
      "age": 39,
      "gender": "male",
      "city": "Buenos Aires",
      "country": "Argentina"
    },
    "shipping": {
      "status": "PENDING",
      "cost": 10,
      "name": "Home delivery",
      "address": "Fake street 968"
    },
    "payment": {
      "status": "approved",
      "status_detail": "Approved on 01/06/2018",
      "type": "CREDIT_CARD",
      "id": 4555887
    }
  },
  {
    "id": 24,
    "total": 985
    "currency": "ARS",
    "status": "open",
    "items": [
      {
        "product_variant_id: 78,
        "quantity": 15
      }
    ],
    "customer": {
      "email": "markjohnson@fakemail.com"
      "name": "Mark Johnson",
      "phone": "16 9547 63214",
      "age": 27,
      "gender": "male",
      "city": "Chicago",
      "country": "United States"
    },
    "shipping": {
      "status": null,
      "cost": null,
      "name": null,
      "address": null
    },
    "payment": {
      "status": null,
      "status_detail": null,
      "type": null,
      "id": null
    }
  }
]
```

### GET /orders?customer_email={CUSTOMER_EMAIL}

Returns a list of orders for a specific customer.

`GET /orders?customer_email=markjohnson@fakemail.com`

```
[
  {
    "id": 24,
    "total": 985
    "currency": "ARS",
    "status": "open",
    "items": [
      {
        "product_variant_id: 78,
        "quantity": 15
      }
    ],
    "customer": {
      "email": "markjohnson@fakemail.com"
      "name": "Mark Johnson",
      "phone": "16 9547 63214",
      "age": 27,
      "gender": "male",
      "city": "Chicago",
      "country": "United States"
    },
    "shipping": {
      "status": null,
      "cost": null,
      "name": null,
      "address": null
    },
    "payment": {
      "status": null,
      "status_detail": null,
      "type": null,
      "id": null
    }
  }
]
```

### GET /orders/{ORDER_ID}

Returns a single order.  

`GET /orders/24`

```
{
  "id": 23,
  "total": 200.5
  "currency": "USD",
  "status": "closed",
  "items": [
    {
      "product_variant_id: 1,
      "quantity": 20
    },
    {
      "product_variant_id": 4,
      "quantity": 6
    }
  ],
  "customer": {
    "email": "pauleriksen@fakemail.com"
    "name": "Paul Eriksen",
    "phone": "11 3695 2548",
    "age": 39,
    "gender": "male",
    "city": "Buenos Aires",
    "country": "Argentina"
  },
  "shipping": {
    "status": "PENDING",
    "cost": 10,
    "name": "Home delivery",
    "address": "Fake street 968"
  },
  "payment": {
    "status": "approved",
    "status_detail": "Approved on 01/06/2018",
    "type": "CREDIT_CARD",
    "id": 4555887
  }
}
```

## POST /orders

The mandatory fields for creating and order are `ID`, `total`, `currency`, `items` and `customer` (is necesary to send a valid customer, which means sending at least the `email` field). When creating an order, the order´s customer will be created automatically with the order. If everything goes ok you will receive the same order in response.

Creating a new order:

### POST /orders

**Body:**

```
{
  "id": 30,
  "total": 300
  "currency": "USD",
  "items": [
    {
      "product_variant_id: 25,
      "quantity": 2
    }
  ],
  "customer": {
    "email": "johnrichards@fakemail.com"
  }
}
```

**Response:**

```
{
  "id": 30,
  "total": 300
  "currency": "USD",
  "status": null,
  "items": [
    {
      "product_variant_id: 25,
      "quantity": 2
    }
  ],
  "customer": {
    "email": "johnrichards@fakemail.com"
    "name": null,
    "phone": null,
    "age": null,
    "gender": null,
    "city": null,
    "country": null
  },
  "shipping": {
    "status": null,
    "cost": null,
    "name": null,
    "address": null
  },
  "payment": {
    "status": null,
    "status_detail": null,
    "type": null,
    "id": null
  }
}
```

## PUT /orders

The only updatable fields of the order are the `status`, `shipping` and `payment`. To update the customer check [Customers](Customers.md). The `ID` is specified on the URL, so it can´t be present in the body object. 

### PUT /orders/{ORDER_ID}

Updating an order..

`PUT /orders/30`  

**Body:**

```
{
  "status": "closed",
  "shipping": {
    "name": "Store pick up",
    "cost": 0
  }
  "payment": {
    "id": 12866,
    "status": "approved",
    "type": "CREDIT_CARD"
  }
}
```

**Response:**

```
{
  "id": 30,
  "total": 300
  "currency": "USD",
  "status": "closed",
  "items": [
    {
      "product_variant_id: 25,
      "quantity": 2
    }
  ],
  "customer": {
    "email": "johnrichards@fakemail.com"
    "name": null,
    "phone": null,
    "age": null,
    "gender": null,
    "city": null,
    "country": null
  },
  "shipping": {
    "name": "Store pick up",
    "cost": 0,
    "name": null,
    "address": null
  }
  "payment": {
    "status": "approved",
    "status_detail": null,
    "type": "CREDIT_CARD",
    "id": 12866,
  }
}
```

## Orders can´t be deleted



