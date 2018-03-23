# Notifications

This module will allow you to send push notifications to multiple customers 
simultaneously.

## Notification properties

| Property  | Description |
| ------------- | ------------- |
| emails  | Array containing all the emails of the customers targeted for the notification. The maximum length for the array is `100`.  |
| title  |  Notification header. |
| body | Notification text message.  |
| action | Object containing the fields `type` and `value`. The posible values for `type` are `category`, `product` and `view` (a specfic view of the App), while the field `value` will contain the `ID` for the specified type. In case you intend to target a `view`, get in touch with our stuff to know which are the allowed values.  |

# Endpoint

## POST /customers/notifications

Creating a notification. All the fields from the notification must be completed. Remember that all the customers wih the specified emails should be already created. If everything goes ok, you will receive the same notification in response.

`POST /customers/notifications`

**Body:**

```
{
  "emails": ["markjohnson@fakemail.com", "taniaperez@fakemail.com"],
  "title": "Take advantage of our new offers!",
  "body": "On this September, we have 25% of discount in all summer clothes.",
  "action": {
    "type": "category",
    "value": 56637
  }
}
```

**Response:**

```
{
  "emails": ["markjohnson@fakemail.com", "taniaperez@fakemail.com"],
  "title": "Take advantage of our new offers!",
  "body": "On this September, we have 25% of discount in all summer clothes.",
  "action": {
    "type": "category",
    "value": 56637
  }
}
```
