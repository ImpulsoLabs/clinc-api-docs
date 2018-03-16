# Brands

## Properties

| Property  | Description |
| ------------- | ------------- |
| id  | Brand `ID` in your eCommerce  |
| name  |  Brand name (for Brands the name is not multilanguage) |
| image_url  | URL of the brand logo (OPTIONAL)  |

# Endpoints

## GET /brands

Receive a list of all the Brands.  

**Parameters:**

| Param  | Description |
| ------------- | ------------- |
| page  | Page number (Default 1)  |
| page_size  |  Size of the page (Maximum 50, Default 10) |

### GET /brands

Returns a list of all the brands.

`GET /brands`

```
[
  {
    "id": 1,
    "name": "My first brand",
    "image_url": "brands.com/firstbrand.jpg"
  },
  {
    "id": 2,
    "name": "My second brand",
    "image_url": "brands.com/secondbrand.jpg"
  },
  {
    "id": 3,
    "name": "No image brand",
    "image_url": null
  }
]
```

### GET /brands/{BRAND_ID}

Returns a single brand.

`GET /brands/1`

```
{
  "id": 1,
  "name": "My first brand",
  "image_url": "brands.com/firstbrand.jpg"
}
```

## POST /brands

For creating brands, only the `ID` and the `name` are mandatory. If everything goes ok, you will receive the same brand in response.

### POST /brands

**Body:**

```
{
  "id": 1,
  "name": "My first brand",
  "image_url": "brands.com/firstbrand.jpg"
}
```

**Response:**

```
{
  "id": 1,
  "name": "My first brand",
  "image_url": "brands.com/firstbrand.jpg"
}
```

## PUT /brands

The `ID` of the brand to update is specified in the URL, so it can´t appear inside the body object.

### PUT /brands/{BRAND_ID}

`PUT /brands/2`

**Body:**

```
{
  "name": "My second brand is renamed"
}
```

**Response:**

```
{
  "id": 2,
  "name": "My second brand is renamed",
  "image_url": "brands.com/secondbrand.jpg"
}
```

## DELETE /brands

Brands are deleted individually by `ID`. The `ID` is specified on the URL. When deleting a brand **all products associated to the brand will be deleted too**. The successful response is an empty object.

### DELETE /brands/{BRAND_ID}

`DELETE /brands/1`


**Response:**

```
{}
```




