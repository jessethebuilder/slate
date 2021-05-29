# Orders

## Get Many Orders

```ruby
  RestClient.get(
    "http://localhost:3000/orders",
    authorization: "Token #{@token}",
    accept: :json
  )
```
```shell
curl "http://localhost:3000/orders.json" \
  -H "Authorization: Token test_token"
```
```elixir
HTTPoison.get!(
  "http://localhost:3000/orders",
  [
    "Authorization": "Token test_token",
    "ACCEPT": "application/json",
    "Content-Type": "application/json"
  ]
)
```

> The above command returns a status of 200 and JSON structured like this:

```json
[
  {
    "id": 4,
    "order_items": [
      {
        "id": 13,
        "amount": 19440,
        "note": "Fuga neque velit eos.",
        "data": {
        },
        "order_id": 4,
        "product_id": 36,
        "product_name": "Poutine",
        "group_name": "Kids",
        "created_at": "2021-05-28T21:01:36.149Z",
        "updated_at": "2021-05-28T21:01:36.149Z"
      },
    ],
    "total": 66248,
    "subtotal": 66248,
    "tax": 0,
    "tip": 0,
    "data": {
    },
    "customer_id": 2,
    "menu_id": null,
    "menu_name": null,
    "note": "Soluta maiores et exercitationem.",
    "seen_at": null,
    "funded_at": null,
    "delivered_at": null,
    "created_at": "2021-05-28T22:23:52.520Z",
    "updated_at": "2021-05-28T22:23:52.553Z"
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
  Don't forget to URL encode your Date/time params.
</aside>

## Get an Order

```ruby
RestClient.get(
  "http://localhost:3000/orders/#{order_id}",
  authorization: "Token #{@token}",
  accept: :json
)
```

```shell
curl "http://localhost:3000/orders/[order_id].json" \
  -H "Authorization: Token test_token"
```

```elixir
HTTPoison.get!(
  "http://localhost:3000/orders/[order_id]",
  [
    "Authorization": "Token token_test",
    "ACCEPT": "application/json",
    "Content-Type": "application/json"
  ]
)
```

```json
{
  "id": 4,
  "order_items": [
    {
      "id": 13,
      "amount": 19440,
      "note": "Fuga neque velit eos.",
      "data": {
      },
      "order_id": 4,
      "product_id": 36,
      "product_name": "Poutine",
      "group_name": "Kids",
      "created_at": "2021-05-28T21:01:36.149Z",
      "updated_at": "2021-05-28T21:01:36.149Z"
    },
  ],
  "total": 66248,
  "subtotal": 66248,
  "tax": 0,
  "tip": 0,
  "data": {
  },
  "customer_id": 2,
  "menu_id": null,
  "menu_name": null,
  "note": "Soluta maiores et exercitationem.",
  "seen_at": null,
  "funded_at": null,
  "delivered_at": null,
  "created_at": "2021-05-28T22:23:52.520Z",
  "updated_at": "2021-05-28T22:23:52.553Z"
}
```

### HTTP Request

`GET http://localhost:3000/orders/[order_id]`

### URL Parameters

Parameter | Description
--------- | -----------
order_id | The ID of the Order

## Create an Order

```ruby
RestClient.post(
  "http://localhost:3000/orders",
  {order: note: 'A Note.'},
  authorization: "Token #{@token}",
  accept: :json
)
```

```shell
curl "http://localhost:3000/orders.json" \
  -X POST \
  -d 'order[note]=A Note.' \
  -H "Authorization: Token test_token"
```

```elixir
HTTPoison.post!(
  "http://localhost:3000/orders",
  %{order: %{note: 'A Note.'}},
  [
    "Authorization": "Token test_token",
    "ACCEPT": "application/json",
    "Content-Type": "application/json"
  ]
)
```

```json
{
  "id": 4,
  "order_items": [
    {
      "id": 13,
      "amount": 19440,
      "note": "Fuga neque velit eos.",
      "data": {
      },
      "order_id": 4,
      "product_id": 36,
      "product_name": "Poutine",
      "group_name": "Kids",
      "created_at": "2021-05-28T21:01:36.149Z",
      "updated_at": "2021-05-28T21:01:36.149Z"
    },
  ],
  "total": 66248,
  "subtotal": 66248,
  "tax": 0,
  "tip": 0,
  "data": {
  },
  "customer_id": 2,
  "menu_id": null,
  "menu_name": null,
  "note": "A Note.",
  "seen_at": null,
  "funded_at": null,
  "delivered_at": null,
  "created_at": "2021-05-28T22:23:52.520Z",
  "updated_at": "2021-05-28T22:23:52.553Z"
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

### OrderItem Parameters

OrderItem Parameters are an Array of objects held within the `order_items` key of
the `order` key of your POST data

Parameter | Description | Type
--------- | ----------- | ----
product_id | | Integer
amount | Amount in cents | Integer
note | | String

## Delete an Order

```ruby
  RestClient.delete(
    "#{url_base}/orders/[order_id]",
    authorization: "Token #{@token}",
    accept: :json
  )
```
```shell
curl "http://localhost:3000/orders/[order_id].json" \
  -X DELETE \
  -H "Authorization: Token test_token"
```

```elixir
HTTPoison.delete!(
  "http://localhost:3000/orders/[order_id]",
  [
    "Authorization": "Token test_token",
    "ACCEPT": "application/json",
    "Content-Type": "application/json"
  ]
)
```

### HTTP Request

`DELETE http://localhost:3000/orders/[order_id]`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Order to delete
