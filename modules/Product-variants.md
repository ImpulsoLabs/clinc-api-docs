# Product variants

## Properties

| Property  | Description |
| ------------- | ------------- |
| id  | Product variant `ID` in your eCommerce  |
| attributes_values | Hashmap for each value of the `attributes` specified in the product. Example: { "Size": "SM", "Color": "Black" }. (MULTILANGUAGE)  |
| images | Array of URLs. |
| price | Default price. |
| promotional_price | Will replace the price if the starting and ending  dates are valid. (OPTIONAL) |
| promotional_price_start_date | Date since the promotional price is valid. (OPTIONAL, required if `promotional_price` is present) |
| promotional_price_end_date | Date until the promotional price expires. (OPTIONAL, required if `promotional_price` is present) |
| weight | Product variant weight. (OPTIONAL) |
| width | Product variant width. (OPTIONAL) |
| height | Product variant height. (OPTIONAL) |
| stock_type | Values: UNLIMITED (unlimited stock), LIMITED (stock limited and represented by the field `stock`) or NO_STOCK (stock cero) 
| stock | Required for `stock_type` LIMITED. |
| ean13 | String with length of 13 characters. Used for QA scanner. (OPTIONAL) |

# Endpoints

## GET /products/{PRODUCT_ID}/variants

Product variants are not paginated.  

`GET /products/1/variants`

```
[
  {
    "id": "2",
    "attributes_values": { "Size": "XL", "Color": "Red" },
    "images": ["images.com/xl-red-image1.jpg", "images.com/xl-red-image2.jpg"],
    "price": 100,
    "promotional_price": 80,
    "promotional_price_start_date": "2018-01-01",
    "promotional_price_end_date": "2018-06-01",
    "stock_type": "LIMITED",
    "stock": 10,
    "weight": 100,
    "width": 20,
    "height": null,
    "ean13": "8032939781738"
  },
  {
    "id": "3",
    "attributes_values": { "Size": "M", "Color": "Blue" },
    "images": ["images.com/m-blue-image1.jpg", "images.com/m-blue-image2.jpg"],
    "price": 120,
    "promotional_price": null,
    "promotional_price_start_date": null,
    "promotional_price_end_date": null,
    "stock_type": "UNLIMITED",
    "stock": null,
    "weight": null,
    "width": null,
    "height": null,
    "ean13": null
  }
]
```

### GET /products/{PRODUCT_ID}/variants/{PRODUCT_VARIANT_ID}

Returns a single product variant.  

`GET /products/1/variants/2`

```
{
  "id": "2",
  "attributes_values": { "Size": "XL", "Color": "Red" },
  "images": ["images.com/xl-red-image1.jpg", "images.com/xl-red-image2.jpg"],
  "price": 100,
  "promotional_price": 80,
  "promotional_price_start_date": "2018-01-01",
  "promotional_price_end_date": "2018-06-01",
  "stock_type": "LIMITED",
  "stock": 10,
  "weight": 100,
  "width": 20,
  "height": null,
  "ean13": "8032939781738"
}
```

## POST /products/{PRODUCT_ID}/variants

Product variants can be created with the product (at least 1 is required to create the product) but you can add more later.

Creating a new product variant:

### POST /products/{PRODUCT_ID}/variants

**Body:**

```
{
  "id": "2",
  "attributes_values": { "Size": "XL", "Color": "Red" },
  "images": ["images.com/product-variant-image1.jpg", "images.com/product-variant-image2.jpg"],
  "price": 100,
  "stock_type": "UNLIMITED"
}
```

**Response:**

```
{
  "id": "2",
  "attributes_values": { "Size": "XL", "Color": "Red" },
  "images": ["images.com/product-variant-image1.jpg", "images.com/product-variant-image2.jpg"],
  "price": 100,
  "promotional_price": null,
  "promotional_price_start_date": null,
  "promotional_price_end_date": null,
  "stock_type": "UNLIMITED",
  "stock": null,
  "weight": null,
  "width": null,
  "height": null,
  "ean13": null
}
```

## PUT /products/{PRODUCT_ID}/variants/{PRODUCT_VARIANT_ID}

Product variants are updated individually by `ID` specified on the URL, so it can´t be present in the body object. The only fields which are not updatable are `ID` and `attributes_values`. The field `images` if added, will replace the entire previous array for the new one. 

### PUT /products/{PRODUCT_ID}/variants/{PRODUCT_VARIANT_ID}

Updating a product variant.

`PUT /products/1/variants/2`  

**Body:**

```
{
  "images": ["images.com/my-new-and-only-image.jpg"],
  "price": 120,
  "stock_type": "LIMITED"
  "stock": 20,
  "weight": 23,
  "height": 3565,
  "ean13": "6587423659874"
}
```

**Response:**

```
{
  "id": "2",
  "attributes_values": { "Size": "XL", "Color": "Red" },
  "images": [images.com/my-new-and-only-image.jpg"],
  "price": 120,
  "promotional_price": null,
  "promotional_price_start_date": null,
  "promotional_price_end_date": null,
  "stock_type": "LIMITED",
  "stock": 20,
  "weight": 23,
  "width": null,
  "height": 3565,
  "ean13": "6587423659874"
}
```

## DELETE /products

Product variants are deleted individually by `ID`. The `ID` is specified on the URL and the successful response is an empty object.

### DELETE /products/{PRODUCT_ID}/variants/{PRODUCT_VARIANT_ID}


`DELETE /products/1/variants/2`  

**Response:**

```
{}
```




