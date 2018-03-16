# Products

## Properties

| Property  | Description |
| ------------- | ------------- |
| id  | Product `ID` in your eCommerce  |
| name  |  Product name (MULTILANGUAGE) |
| attributes | Array for the attributes of the product (Size, Color,..) (MULTILANGUAGE)  |
| brand_id | `ID` of the product´s brand |
| categories_ids | Array containing the `IDs` of the categories which the product belongs |
| custom_fields | Hashmap for aditional information you may wanna send (OPTIONAL) |
| product_variants | Array. Product variants can be added,updated or deleted individually later, but you can also create them at the same time with the product. Actually, to create a product successfuly, at least one product variant must be in present in the array. Check [Product Variants](Product-variants.md) to know the product variant object data fields.  |

# Endpoints

## GET /products

Products are paginated.  

**Parameters:**

| Param  | Description |
| ------------- | ------------- |
| brand_id  | `ID` of the Brand. |
| category_id  | `ID` of the Category. |
| page  | Page number (Default 1)  |
| page_size  |  Size of the page (Maximum 50, Default 10) |


### GET /products

Returns a list of products

`GET /products?brand_id=1`

```
[
  {
    "id": 1,
    "name": "My first product",
    "attributes": ["Size", "Color"],
    "brand": {
      "id": 1,
      "name": "My first brand",
      "image_url": "brands.com/firstbrand.jpg"
    },
    "categories": [
      {
        "id": 3,
        "name": "Subcategory 1 with no images",
        "images": [],
        "subcategories": [
          .
          .
          .
        ]
      },
      {
        "id": 4,
        "name": "Subcategory 2 with no subcategories",
        "images": ["subcategories.com/subcategory2.jpg"],
        "subcategories": []
      }
    ],
    "custom_fields": { "Secondary color": "blue" },
    "product_variants": [
      .
      .
      .
    ]
  }
]
```

### GET /products/{PRODUCT_ID}

Returns a single product.  

`GET /products/1`

```
{
  "id": 1,
  "name": "My first product",
  "attributes": ["Size", "Color"],
  "brand": {
    "id": 1,
    "name": "My first brand",
    "image_url": "brands.com/firstbrand.jpg"
  },
  "categories": [
    {
      "id": 3,
      "name": "Subcategory 1 with no images",
      "images": [],
      "subcategories": [
        .
        .
        .
      ]
    },
    {
      "id": 4,
      "name": "Subcategory 2 with no subcategories",
      "images": ["subcategories.com/subcategory2.jpg"],
      "subcategories": []
    }
  ],
  "custom_fields": { "Secondary color": "blue" },
  "product_variants": [
    .
    .
    .
  ]
}
```

## POST /products

Products are created individually. The mandatory fields are `ID`, `attributes`, `brand_id` and `product_variants` (at least one is required). If everything goes ok, you will receive the same product in response.

**Creating a new product:**

### POST /products

**Body:**

```
{
  "id": 5,
  "name": "My new product",
  "attributes": ["Size, "Color"],
  "brand_id": 1,
  "categories_ids": [1,3,4],
  "product_variants": [
    {
      "id": "2",
      "attributes_values": { "Size": "XL", "Color": "Red" },
      "images": ["images.com/product-variant-image1.jpg", "images.com/product-variant-image2.jpg"],
      "price": 100,
      "promotional_price": 80,
      "promotional_price_start_date": "2018-01-01",
      "promotional_price_end_date": "2018-06-01",
      "stock_type": "LIMITED",
      "stock": 10
    }
  ]
}
```

**Response:**

```
{
  "id": 5,
  "name": "My new product",
  "attributes": ["Size", "Color"],
  "brand": {
    "id": 1,
    "name": "My first brand",
    "image_url": "brands.com/firstbrand.jpg"
  },
  "categories": [
    {
      "id": 1,
      "name": "Category 1",
      "images": ["categories.com/category1.jpg", "categories.com/category1SecondImage.jpg"],
      "subcategories": [
        .
        .
      ]
    },
    {
      "id": 3,
      "name": "Subcategory 1 with no images",
      "images": [],
      "subcategories": [
        .
        .
      ]
    },
    {
      "id": 4,
      "name": "Subcategory 2 with no subcategories",
      "images": ["subcategories.com/subcategory2.jpg"],
      "subcategories": []
    }
  ],
  "custom_fields": null,
  "product_variants": [
    {
      "id": "2",
      "attributes_values": { "Size": "XL", "Color": "Red" },
      "images": ["images.com/product-variant-image1.jpg", "images.com/product-variant-image2.jpg"],
      "price": 100,
      "promotional_price": 80,
      "promotional_price_start_date": "2018-01-01",
      "promotional_price_end_date": "2018-06-01",
      "stock_type": "LIMITED",
      "stock": 10,
      "weight": null,
      "width": null,
      "ean13": null
    }
  ]
}
```

## PUT /products

Products are updated individually by `ID` specified on the URL, so it can´t be present in the body object. The fields `ID` and `attributes` are not updatable. For adding, updating or deleting product variants go to [Product Variants](Product-variants.md). The field `categories_ids` if added, will replace the entire provious array for the new one. 

### PUT /products/{PRODUCT_ID}

Updating a product.

`PUT /products/1`  

**Body:**

```
{
  "name": "Product new name",
  "brand_id": 2,
  "categories_ids": [3]
}
```

**Response:**

```
{
  "id": 1,
  "name": "Product new name",
  "attributes": ["Size", "Color"],
  "brand": {
    "id": 2,
    "name": "My second brand",
    "image_url": "brands.com/secondbrand.jpg"
  },
  "categories": [
    {
      "id": 3,
      "name": "Subcategory 1 with no images",
      "images": [],
      "subcategories": [
        .
        .
        .
      ]
    }
  ],
  "custom_fields": { "Secondary color": "blue" },
  "product_variants": [
    .
    .
    .
  ]
}
```

## DELETE /products

Products are deleted individually by `ID`. The `ID` is specified on the URL and the successful response is an empty object.
When deleting a product, all it´s product variants are deleted too.

### DELETE /products/{PRODUCT_ID}


`DELETE /products/1`  

**Response:**

```
{}
```




