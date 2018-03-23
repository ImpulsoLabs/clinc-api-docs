# Store

## Configurable properties

| Property  | Description |
| ------------- | ------------- |
| checkout_url  | At this url we will do a POST at the moment of the checkout, sending as body all the variants purchased in the order with their respective quantities, example: `[{ "product_variant_id": 123, "quantity": 1 }, ..]`. The request must return an object with the URL which we will redirect the user to finish the checkout, example: `{ "url": "mystore.com/checkout" }`.   |
| currency  |  Store default currency. Check [Currency ISO values](http://www.xe.com/iso4217.php). |
| language | Store default language. Supported: english `(en)`, spanish `(es)` and portuguese `(pt)`.  |

# Endpoint

## PUT /store

Updating store configuration. You don´t need to send all the properties, just the ones you want to update. If everything goes ok you will receive your current configuration as response.

**Body:**

```
{
  "checkout_url": "mystore.com/process-checkout",
  "currency": "USD"
}
```

**Response:**

```
{
  "checkout_url": "mystore.com/process-checkout",
  "currency": "USD",
  "language": "en"
}
```
