---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - elixir

toc_footers:
  - <a href='http://localhost:3000.com'>Sign Up for a Developer Key</a>

includes:
  - orders
  - transactions
  - products
  - groups
  - menus
  - customers
  - notifications

search: true

code_clipboard: true
---

# The Forge API

The Forge is designed to serve as a persistence layer, payment processor,
and notification service for simple eCommerce applications.

Developers and designers can focus on domain specifics while still being able to
save and create orders, send notifications to app-owners and customers, process
payments, and store/serve data commerce-related data via this API.

Please see [The Forge](http://localhost:3000.com) for detials on how to set up an Account
and get an API Token.

# Authentication

> To authorize, use this code:

```shell
curl "http://localhost:3000/[api_endpoint].json" \
  -H "Authorization: Token test_token"
```

```ruby
  RestClient.get(
    "http://localhost:3000/[api_endpoint]",
    authorization: "Token #{@token}",
    accept: :json
  )
```

```elixir
HTTPoison.get!(
  "http://localhost:3000/[api_endpoint]",
  [
    "Authorization": "Token test_token",
    "ACCEPT": "application/json",
    "Content-Type": "application/json"
  ]
)
```

The Forge expects the API Token to be included in all API requests:

`Authorization: Token test_token`

<aside class="notice">
  Replace "test_token" with your API Token in API calls.
</aside>
