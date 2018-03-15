# Read before
This API does not include the registration process. To create your store at Clinc! please get in touch with our stuff, for more information check [clincshop.com](http://clincshop.com).

# Aunthentication + Making requests
API base url: `https://admin.clincshop.com/clincapi/v1/..`  
Once you have a store at Clinc!, our stuff will provide you an access token which you will need for authentication. To authenticate, you will have to send your access token as a header in all your requests:  

```
curl -H 'access-token:{MY_ACCESS_TOKEN}' \
     https://admin.clincshop.com/clincapi/v1/products
```

# Data type: JSON
For both sending and receiving data we use only JSON objects, so you will have to send `Content-Type: application/json' as a header too.  
So actually, the requests will look like this:

```
curl -H 'access-token:{MY_ACCESS_TOKEN}' \
     -H 'Content-Type: application/json' \
     https://admin.clincshop.com/clincapi/v1/products
```

# Client errors
These are the possible types of client errors on API calls that receive request bodies:  

- Sending invalid JSON will result in a `400 Bad Request` response.

```
HTTP/1.1 400 Bad Request

{ 
  "error": "Invalid JSON"
}
```

- Sending and invalid entity will result in a 422 Unprocessable Entity response.

```
HTTP/1.1 422 Unprocessable Entity

{
  "name": "Can't be blank"
}
```

# Server errors
If Clinc! is having trouble, you might see a 5xx error. 500 means that the app is entirely down, but you might also see `502 Bad Gateway`, `503 Service Unavailable`, or `504 Gateway Timeout`. It's your responsibility in all of these cases to retry your request later.

#Pagination
Requests that return multiple items will be paginated. You can specify further pages with the `page` parameter. You can also set a custom page size up to 50 with the `page_size` parameter. The `page` number will be 1 by default and the `page_number` will be 10.

```
curl -H 'access-token:{MY_ACCESS_TOKEN}' \
     -H 'Content-Type: application/json' \
     https://admin.clincshop.com/clincapi/v1/products?page=2&page_size=8
```

# Languages
Stores can potentially have multiple languages. This means that some properties will be objects detailing the value for each language (both for GETting and POSTing/PUTing data).  
Example:

```
curl -H 'access-token:{MY_ACCESS_TOKEN}' \
     -H 'Content-Type: application/json' \
     https://admin.clincshop.com/clincapi/v1/products/123

{
    "id": 123,
    "name": {
        "es": "Nombre del producto",
        "pt": "Nome do produto",
        "en": "Product name"
    }
    .
    .
    .
}
```

When POSTing or PUTing data you can provide an object with a value for each language:

```
curl -H 'access-token:{MY_ACCESS_TOKEN}' \
     -H 'Content-Type: application/json' \
     -d '{ "name": {"es": "Nombre", "pt": "Nome", "en": "name"} }' \
     https://admin.clincshop.com/clincapi/v1/products


```

Or you can simply provide a string value, which will be applied to all the languages:

```
curl -H 'access-token:{MY_ACCESS_TOKEN}' \
     -H 'Content-Type: application/json' \
     -d '{ "name": "Nombre" }' \
     https://admin.clincshop.com/clincapi/v1/products
```

# API Features
- [Brands](features/Brands.md)
- [Categories](features/Categories.md)
- [Products](features/Products.md)
- [Product variants](features/Product-variants.md)
- [Product pictures](features/Product-pictures.md)
- [Orders](features/Orders.md)
- [Customers](features/Customers.md)
- [Notifications](features/Notifications.md)





