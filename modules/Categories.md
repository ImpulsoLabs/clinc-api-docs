# Categories

## Properties

| Property  | Description |
| ------------- | ------------- |
| id  | Category `ID` in your eCommerce  |
| name  |  Category name (Multilanguage) |
| images | Array of URLs. A category may have multiple images. (OPTIONAL)  |
| parent_id | `ID` of the parent category. Categories can only have one parent. |

# Endpoints

## GET /categories

Categories are not paginated.  

**Parameters:**

| Param  | Description |
| ------------- | ------------- |
| parent_id  | `ID` of the parent category.  |

### GET /categories

Returns the entire categories tree.  

`GET /categories`

```
[
  {
    "id": 1,
    "name": "Category 1",
    "images": ["categories.com/category1.jpg", "categories.com/category1SecondImage.jpg"],
    "subcategories": [
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
    ]
  },
  {
    "id": 2,
    "name": "Category 2 with no subcategories",
    "images": ["categories.com/category2.jpg"],
    "subcategories": []
  }
]
```

### GET /categories?parent_id={CATEGORY_ID}

Returns all the categories with the specified parent `ID`. For getting the root categories, use `parent_id=null`.

`GET /categories?parent_id=1`

```
[
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
]
```

### GET /categories/{CATEGORY_ID}

Returns a single category.

`GET /categories/4`

```
{
  "id": 4,
  "name": "Subcategory 2 with no subcategories",
  "images": ["subcategories.com/subcategory2.jpg"],
  "subcategories": []
}
```


## POST /categories

For creating categories, only the `ID` and the `name` are mandatory. If everything goes ok, you will receive the same category in response. For creating root categories, omit the `parent_id` field.


**Creating a root category:**

### POST /categories

`POST /categories`

**Body:**

```
{
  "id": 1,
  "name": "Category 1",
  "images": ["categories.com/category1.jpg", "categories.com/category1SecondImage.jpg"]
}
```

**Response:**

```
{
  "id": 1,
  "name": "Category 1",
  "images": ["categories.com/category1.jpg", "categories.com/category1SecondImage.jpg"],
  "subcategories": []
}
```


**Add subcategories to category:**  
  
`/categories`  

**Body:**

```
{
  "id": 4,
  "parent_id": 1,
  "name": "Subcategory 2",
  "images": ["subcategories.com/subcategory2.jpg"]
}
```

**Response:**

```
{
  "id": 4,
  "name": "Subcategory 2",
  "images": ["subcategories.com/subcategory2.jpg"],
  "subcategories": []
}
```

## PUT /categories

Categories are updated individually by `ID` specified on the URL, so it can´t be present in the body object. The `parent_id` can be changed. If you include the field `images` in the object, the new array will replace the previous one (deleting all unrepeated URLs). 

### PUT /categories/{CATEGORY_ID}

Updating a category.

`PUT /categories/1`

**Body:**

```
{
  "name": "New category name",
  "images": ["categories.com/new-picture.jpg"]
}
```

**Response:**

```
{
  "id": 1,
  "name": "New category name",
  "images": ["categories.com/new-picture.jpg"],
  "subcategories":[
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
  ]
}
```

## DELETE /categories

The category `ID` is specified on the URL and the successful response is an empty object.
When deleting a category, all it´s subcategories are deleted too.

### DELETE /categories/{CATEGORY_ID}

`DELETE /categories/1`

**Response:**

```
{}
```




