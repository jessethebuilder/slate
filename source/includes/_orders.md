# Orders

## Get Orders

```ruby
  RestClient.get(
    "http://localhost:3000/orders",
    authorization: "Token <auth_token>",
    accept: :json
  )
```

```shell
curl "http://localhost:3000/orders.json" \
  -H "Authorization: Token <auth_token>"
```

> The above command returns a status of 200 and JSON structured like this:

```json
[
  {
    "id": 4,
    "order_items": [
      {
        "id": 15,
        "amount": 41398,
        "note": "Dolorem doloribus magni dolor.",
        "data": {
          "some": "info about this"
        },
        "order_id": 4,
        "product_id": 29,
        "product_name": "Chicken Fajitas",
        "group_id": 7,
        "group_name": "Beauty",
        "menu_id": 2,
        "menu_name": "Necessities",
        "created_at": "2021-06-02T03:48:21.822Z",
        "updated_at": "2021-06-02T04:29:15.885Z"
      }
    ],
    "transactions": [
      {
        "id": 2,
        "amount": 41398,
        "transaction_type": "charge",
        "order_id": 4,
        "stripe_id": "ch_1IxgiK2eZvKYlo2CpTEzk6ra",
        "created_at": "2021-06-02T04:29:40.253Z",
        "updated_at": "2021-06-02T04:35:28.977Z"
      }
    ],
    "total": 41398,
    "subtotal": 41398,
    "tax": 0,
    "tip": 0,
    "data": {
      "hello": "world"
    },
    "customer_id": 2,
    "menu_id": null,
    "menu_name": null,
    "note": "Eveniet vitae voluptatum quod.",
    "seen_at": null,
    "delivered_at": null,
    "created_at": "2021-06-02T03:48:21.756Z",
    "updated_at": "2021-06-02T04:25:16.462Z"
  }
]
```

### HTTP Request

`GET http://localhost:3000/api/orders`

### Query Parameters

Parameter | Default | Description | Format
--------- | ------- | ----------- | ------
page | 1 | Pagination page |
per_page | 100 | Per pagination page |
created_on | null | Returns Orders from the beginning to end of the date provided | yyyy-mm-dd
created_after | null | Returns Orders after the Date or Datetime provided | yyyy-mm-dd (hh:mm:ss:mmmm)
created_before | null | Returns Orders before the Date or Datetime provided | yyyy-mm-dd (hh:mm:ss:mmmm)

<aside class="notice">
  Don't forget to URL encode your params. Especially Dates and Datetimes.
</aside>

## Get an Order

```ruby
RestClient.get(
  "http://localhost:3000/orders/#{order_id}",
  authorization: "Token <auth_token>",
  accept: :json
)
```

```shell
curl "http://localhost:3000/orders/<order_id>.json" \
  -H "Authorization: Token <auth_token>"
```

> The above command returns a status of 200 and JSON structured like this:

```json
{
  "id": 4,
  "order_items": [
    {
      "id": 15,
      "amount": 41398,
      "note": "Dolorem doloribus magni dolor.",
      "data": {
        "some": "info about this"
      },
      "order_id": 4,
      "product_id": 29,
      "product_name": "Chicken Fajitas",
      "group_id": 7,
      "group_name": "Beauty",
      "menu_id": 2,
      "menu_name": "Necessities",
      "created_at": "2021-06-02T03:48:21.822Z",
      "updated_at": "2021-06-02T04:29:15.885Z"
    }
  ],
  "transactions": [
    {
      "id": 2,
      "amount": 41398,
      "transaction_type": "charge",
      "order_id": 4,
      "stripe_id": "ch_1IxgiK2eZvKYlo2CpTEzk6ra",
      "created_at": "2021-06-02T04:29:40.253Z",
      "updated_at": "2021-06-02T04:35:28.977Z"
    }
  ],
  "total": 41398,
  "subtotal": 41398,
  "tax": 0,
  "tip": 0,
  "data": {
    "hello": "world"
  },
  "customer_id": 2,
  "menu_id": null,
  "menu_name": null,
  "note": "Eveniet vitae voluptatum quod.",
  "seen_at": null,
  "delivered_at": null,
  "created_at": "2021-06-02T03:48:21.756Z",
  "updated_at": "2021-06-02T04:25:16.462Z"
}
```

### HTTP Request

`GET http://localhost:3000/orders/<order_id>`

### URL Parameters

Parameter | Description
--------- | -----------
*order_id | The ID of the Order

## Create an Order

```ruby
RestClient.post(
  "http://localhost:3000/orders",
  {
    order: {
      note: 'A Note.'
      order_items: [
        {
          amount: 1000,
          product_id: 3
        }
      ]
    }
  },
  authorization: "Token <auth_token>",
  accept: :json
)
```

```shell
curl "http://localhost:3000/orders.json" \
  -X POST \
  -d 'order[note]=A Note.' \
  -H "Authorization: Token <auth_token>"
```

> The above command returns a status of 201 and JSON structured like this:

```json
{
  "id": 4,
  "order_items": [
    {
      "id": 15,
      "amount": 41398,
      "note": "Dolorem doloribus magni dolor.",
      "data": {
        "some": "info about this"
      },
      "order_id": 4,
      "product_id": 29,
      "product_name": "Chicken Fajitas",
      "group_id": 7,
      "group_name": "Beauty",
      "menu_id": 2,
      "menu_name": "Necessities",
      "created_at": "2021-06-02T03:48:21.822Z",
      "updated_at": "2021-06-02T04:29:15.885Z"
    }
  ],
  "transactions": [
    {
      "id": 2,
      "amount": 41398,
      "transaction_type": "charge",
      "order_id": 4,
      "stripe_id": "ch_1IxgiK2eZvKYlo2CpTEzk6ra",
      "created_at": "2021-06-02T04:29:40.253Z",
      "updated_at": "2021-06-02T04:35:28.977Z"
    }
  ],
  "total": 41398,
  "subtotal": 41398,
  "tax": 0,
  "tip": 0,
  "data": {
    "hello": "world"
  },
  "customer_id": 2,
  "menu_id": null,
  "menu_name": null,
  "note": "Eveniet vitae voluptatum quod.",
  "seen_at": null,
  "delivered_at": null,
  "created_at": "2021-06-02T03:48:21.756Z",
  "updated_at": "2021-06-02T04:25:16.462Z"
}
```

### HTTP Request

`POST http://localhost:3000/orders`

### Order Parameters

Order Parameters must be in the `order` key of your POST data

Parameter | Description | Type
--------- | ----------- | ----
note | | String
customer_id | | Integer
menu_id | | Integer
tip | Tip in cents | Integer
tax | Tax in cents | Integer
seen_at | | DateTime
delivered_at | | DateTime
data | Any JSON | JSON
see | Pass "true" to mark seen_at as now | Boolean
order_items | See below | Array

### OrderItems Parameters

OrderItem Parameters are an Array of objects held within the `order_items` key of
the `order` key of your POST data.

Total of OrderItems (and thus Order) must be no less than 50 (cents)

Parameter | Description | Type
--------- | ----------- | ----
*product_id | | Integer
*amount | In cents | Integer
note | | String | false

### Transactions Parameters

Transactions Paramaters are an Array of objects held within the `Transactions` key
of the `order` key of your POST data.

Either a `stripe_token` OR a `card_number` AND `card_expiration` AND `card_ccv`
must be supplied.

Parameter | Description | Type
--------- | ----------- | ----
amount | In cents | Integer
card_number | | String | true
card_expiration | Amount in cents | String
card_ccv | | String
stripe_token | | String

<aside class="notice">
  When creating an Order with valid Transaction params, where the :amount of the Transaction
  is not provided, it will be assumed that the Transaction :amount is the full :amount
  of the Order.
</aside>

### Errors

Errors are returned as a JSON Array with keys of attribute names, and values of
Arrays of related Errors.

```json
{
  "order_items": [
    "Amount must be positive",
    "Product cannot be blank"
  ]
}
```

## Update an Order

There is currently no way to update an Order, though you can create Refund Transactions
via the `/transactions` endpoint.

## Delete an Order

```ruby
  RestClient.delete(
    "http://localhost:3000/orders/<order_id>",
    authorization: "Token <auth_token>",
    accept: :json
  )
```

```shell
curl "http://localhost:3000/orders/<order_id>.json" \
  -X DELETE \
  -H "Authorization: Token <auth_token>"
```

> The above command returns a status of 204 and NOTHING

### HTTP Request

`DELETE http://localhost:3000/orders/<order_id>`

### URL Parameters

Parameter | Description
--------- | -----------
*ID | The ID of the Order to delete
