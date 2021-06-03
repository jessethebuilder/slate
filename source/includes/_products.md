# Products

## Get Products

```ruby
  RestClient.get(
    "http://localhost:3000/products",
    authorization: "Token <auth_token>",
    accept: :json
  )
```
```shell
curl "http://localhost:3000/products.json" \
  -H "Authorization: Token <auth_token>"
```
```elixir
HTTPoison.get!(
  "http://localhost:3000/products",
  [
    "Authorization": "Token <auth_token>",
    "ACCEPT": "application/json",
    "Content-Type": "application/json"
  ]
)
```

> The above command returns a status of 200 and JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Pho",
    "description": "Aut voluptatibus maxime. Id architecto ea. Sed assumenda quo.",
    "order": null,
    "price": 24935,
    "group_id": 1,
    "group_name": "Industrial",
    "menu_id": 1,
    "menu_name": "New Reno",
    "data": {
      "any": "data"
    },
    "active": true,
    "created_at": "2021-06-02T03:48:20.679Z",
    "updated_at": "2021-06-02T03:48:20.679Z"
  }
]
```

### HTTP Request

`GET http://localhost:3000/api/products`

### Query Parameters

Parameter | Default | Description | Format
--------- | ------- | ----------- | ------
scope | active | | all, active, inactive, archived

## Get Product

```ruby
  RestClient.get(
    "http://localhost:3000/products/<product_id>",
    authorization: "Token <auth_token>",
    accept: :json
  )
```

```shell
curl "http://localhost:3000/products.json/<product_id>" \
  -H "Authorization: Token <auth_token>"
```

> The above command returns a status of 200 and JSON structured like this:

```json
{
  "id": 1,
  "name": "Pho",
  "description": "Aut voluptatibus maxime. Id architecto ea. Sed assumenda quo.",
  "order": null,
  "price": 24935,
  "group_id": 1,
  "group_name": "Industrial",
  "menu_id": 1,
  "menu_name": "New Reno",
  "data": {
    "any": "data"
  },
  "active": true,
  "created_at": "2021-06-02T03:48:20.679Z",
  "updated_at": "2021-06-02T03:48:20.679Z"
}
```

### HTTP Request

`GET http://localhost:3000/api/products/<product_id>`

### URL Parameters

Parameter | Description
--------- | -----------
*product_id | The ID of the Product

## Create a Product

```ruby
RestClient.post(
  "http://localhost:3000/products",
  {
    product: {
      name: "Pho",
      description: "Aut voluptatibus maxime. Id architecto ea. Sed assumenda quo.",
      price: 24935,
      group_id: 1,
      menu_id: 1,
      data: {"any" => "data"}
    }
  },
  authorization: "Token <auth_token>",
  accept: :json
)
```

```shell
curl "http://localhost:3000/products.json" \
  -X POST \
  -d 'order[note]=A Note.' \
  -H "Authorization: Token <auth_token>"
```

> The above command returns a status of 201 and JSON structured like this:

```json
{
  "id": 1,
  "name": "Pho",
  "description": "Aut voluptatibus maxime. Id architecto ea. Sed assumenda quo.",
  "order": null,
  "price": 24935,
  "group_id": 1,
  "group_name": "Industrial",
  "menu_id": 1,
  "menu_name": "New Reno",
  "data": {
    "any": "data"
  },
  "active": true,
  "created_at": "2021-06-02T03:48:20.679Z",
  "updated_at": "2021-06-02T03:48:20.679Z"
}
```

### HTTP Request

`POST http://localhost:3000/products`

###  Parameters

Product Parameters must be in the `product` key of your POST data

Parameter | Description | Type
--------- | ----------- | ----
*name | | String
description | | String
*price | in cents | Integer
active | default to true | Boolean
data | Hash data | JSON
order | | Integer
menu_id | | Integer
group_id | | Integer
customer_id | | Integer
menu_id | | Integer

### Errors

Errors are returned as a JSON Array with keys of attribute names, and values of
Arrays of related Errors.

```json
{
  "name": [
    "cannot be blank"
  ]
}
```

## Update a Product

```ruby
RestClient.post(
  "http://localhost:3000/products/<product_id>",
  {
    product: {
      description: "New description."
    }
  },
  authorization: "Token <auth_token>",
  accept: :json
)
```

<!-- ```shell
curl "http://localhost:3000/products/<product_id>.json" \
  -X POST \
  -d 'order[note]=A Note.' \
  -H "Authorization: Token <auth_token>"
``` -->

> The above command returns a status of 201 and JSON structured like this:

```json
{
  "id": 1,
  "name": "Pho",
  "description": "New description.",
  "order": null,
  "price": 24935,
  "group_id": 1,
  "group_name": "Industrial",
  "menu_id": 1,
  "menu_name": "New Reno",
  "data": {
    "any": "data"
  },
  "active": true,
  "created_at": "2021-06-02T03:48:20.679Z",
  "updated_at": "2021-06-02T03:48:20.679Z"
}
```

### HTTP Request

`PUT/PATCH http://localhost:3000/products/<product_id>`

### URL Parameters

Parameter | Description
--------- | -----------
*product_id | The ID of the Product

###  Parameters

Product Parameters must be in the `product` key of your PUT/PATCH data

Parameter | Description | Type
--------- | ----------- | ----
*name | | String
description | | String
*price | in cents | Integer
active | defaults to true | Boolean
archived | defaults to false | Boolean
data | Hash data | JSON
order | | Integer
menu_id | | Integer
group_id | | Integer
customer_id | | Integer
menu_id | | Integer

### Errors

Errors are returned as a JSON Array with keys of attribute names, and values of
Arrays of related Errors.

```json
{
  "name": [
    "cannot be blank"
  ]
}
```

## Delete (or Archive) a Product

A Product associated with ANY OrderItems will not be deleted, but will be archived instead.

```ruby
  RestClient.delete(
    "http://localhost:3000/products/<product_id>",
    authorization: "Token <auth_token>",
    accept: :json
  )
```

<!-- ```shell
curl "http://localhost:3000/products/<product_id>.json" \
  -X DELETE \
  -H "Authorization: Token <auth_token>"
``` -->

> The above command returns a status of 204 and NOTHING

### HTTP Request

`DELETE http://localhost:3000/products/<product_id>`

### URL Parameters

Parameter | Description
--------- | -----------
*ID | The ID of the Product to delete
