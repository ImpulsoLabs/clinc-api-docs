# Before starting
CLINC! is a platform designed to make mobile shopping easier, smarter and more intuitive on both the customer and store’s sides.
Our goal is to integrate an eCommerce with an mCommerce into one sales channel so, at least for now, to integrate with CLINC! (meaning to use this API) you must have already an eCommerce in any platform.  
This API does not include the store creation process. To create your store at CLINC! please get in touch with our staff in [hola@clincshop.com](mailto:hola@clincshop.com).
For more information check [www.clincshop.com](https://www.clincshop.com/?utm_source=github&utm_medium=link&utm_campaign=home) or contact [api@clincshop.com](mailto:api@clincshop.com)

# Aunthentication + Making requests
API base url: `https://admin.clincshop.com/clincapi/v1/..`  
Once you have a store at Clinc!, our stuff will provide you an access token which you will need for authentication. To authenticate, you will have to send your access token as a header in all your requests:  

```
curl -H 'access-token:{MY_ACCESS_TOKEN}' \
     https://admin.clincshop.com/clincapi/v1/products
```

# Data type: JSON
For both sending and receiving data we use only JSON objects, so you will have to send `Content-Type: application/json` as a header too.  
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

- Sending an invalid entity will result in a `422 Unprocessable Entity` response.

```
HTTP/1.1 422 Unprocessable Entity

{
  "name": "Can't be blank"
}
```

# Pagination
Requests that return multiple items will be paginated. You can specify further pages with the `page` parameter. You can also set a custom page size up to 50 with the `page_size` parameter. The `page` number will be 1 by default and the `page_size` will be 10.

```
curl -H 'access-token:{MY_ACCESS_TOKEN}' \
     -H 'Content-Type: application/json' \
     https://admin.clincshop.com/clincapi/v1/products?page=2&page_size=8
```

# Integration with Clinc!
With Clinc! you can integrate your eCommerce with our mCommerce platform, so for most of the entities of this API (`Brands`, `Categories`, `Products`, `Product variants` and `Orders`) we will asume you already have that entity created in your eCommerce, so we will expect you to provide us the `ID` which will be used to match that entity. Thats why for creating these entities in Clinc!, sending the `ID` is mandatory.

# Languages
Stores can potentially have multiple languages. This means that some properties will be objects detailing the value for each language (both for GETting and POSTing/PUTing data). For the properties which support multilanguage, it will be specfied it the entity´s documentation section. Languages supported: english `(en)`, spanish `(es)` and portuguese `(pt)`.
Example:

**Request:**

```
curl -H 'access-token:{MY_ACCESS_TOKEN}' \
     -H 'Content-Type: application/json' \
     https://admin.clincshop.com/clincapi/v1/products/123
```

**Response:**

```
{
    "id": 123,
    "name": {
        "es": "Nombre del producto",
        "pt": "Nome do produto",
        "en": "Product name"
    },
    .
    .
    .
}
```

When POSTing or PUTing data you can provide an object with a value for each language:

```
curl -H 'access-token:{MY_ACCESS_TOKEN}' \
     -H 'Content-Type: application/json' \
     -d '{ "id": 123, "name": {"es": "Nombre", "pt": "Nome", "en": "name"} }' \
     https://admin.clincshop.com/clincapi/v1/products


```

Or you can simply provide a string value, which will be applied to all the languages:

```
curl -H 'access-token:{MY_ACCESS_TOKEN}' \
     -H 'Content-Type: application/json' \
     -d '{ "id": 123, "name": "Nombre" }' \
     https://admin.clincshop.com/clincapi/v1/products
```

# API Modules
- [Store](modules/Store.md)
- [Brands](modules/Brands.md)
- [Categories](modules/Categories.md)
- [Products](modules/Products.md)
- [Product variants](modules/Product-variants.md)
- [Customers](modules/Customers.md)
- [Orders](modules/Orders.md)
- [Notifications](modules/Notifications.md)





