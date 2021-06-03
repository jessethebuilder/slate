# Transactions

Transactions can only be created, according to the following rules:

1. The Transaction must not be between -49 and 49 (so an absolute value of 50 or more).

2. The first Transaction amount for an Order must be for the full amount of the Order total.

3. All subsequent Transactions must be negative (refunds), and the absolute amount of refunds
for a given Order cannot be more than the Order total (or the amount of the first Transaction).


## Create a Transaction

```ruby
RestClient.post(
  "http://localhost:3000/transactions",
  {
    transaction: {

    }
  },
  authorization: "Token <auth_token>",
  accept: :json
)
```

<!-- ```shell
curl "http://localhost:3000/transactions.json" \
  -X POST \
  -d 'order[note]=A Note.' \
  -H "Authorization: Token <auth_token>"
``` -->

> The above command returns a status of 201 and JSON structured like this:

```json
{
  "id": 4,
  "order_id": 5,
  "amount": 1000,
  "transaction_type": "charge",
  "stripe_id": "ch_1IxgiK2eZvKYlo2CpTEzk6ra",
  "created_at": "2021-06-02T03:48:21.756Z",
  "updated_at": "2021-06-02T04:25:16.462Z"
}
```

### HTTP Request

`POST http://localhost:3000/orders/<order_id>/transactions`

### URL Parameters

Parameter | Description
--------- | -----------
*order_id | The ID of the Order

### Transaction Parameters

Transaction Parameters must be in the `transaction` key of your POST data

Either a `stripe_token` OR a `card_number` AND `card_expiration` AND `card_ccv`
must be supplied.

Parameter | Description | Type
--------- | ----------- | ----
*amount | In cents | Integer
card_number | | String | true
card_expiration | Amount in cents | String
card_ccv | | String
stripe_token | | String

### Errors

Errors are returned as a JSON Array with keys of attribute names, and values of
Arrays of related Errors.

```json
{
  "amount": [
    "must be no less than 50"
  ]
}
